# 手写createBrowserHistory

**独特的state处理方式**：目的是不和其他修改state的第三方库互相影响

```js
var historyState = window.history.state;
```

1. 如果historyState没有值，则state为undefined
2. 如果historyState有值
   1. 如果值的类型不是对象
   2. 是对象
      1. 该对象中有key属性，将key属性作为location的key属性值，并且将historyState对象中的state属性作为state属性值
      2. 如果没有key属性，则直接将historyState赋值给state

## 辅助模块

**ListenerManager.js**

```js
export default class ListenerManager {
  //维护一个监听器数组
  listeners = [];

  /**
   * 添加一个监听器，返回一个用于取消监听的函数
   */
  addListener(listener) {
    if (typeof listener !== 'function') {
      throw new TypeError('listener must be a function');
    }
    this.listeners.push(listener);
    return () => {
      this.listeners = this.listeners.filter((lt) => lt !== listener);
    };
  }

  /**
   * 触发所有的监听器
   * @param {*} location
   * @param {*} action
   */
  triggerListener(location, action) {
    if (this.listeners.length === 0) {
      return;
    }
    for (const listener of this.listeners) {
      listener(location, action);
    }
  }
}
```

**BlockManager.js**

```js
export default class BlockManager {
  _block = null; //该属性是否有值，决定了是否有阻塞

  constructor(getUserConfirmation) {
    this.getUserConfirmation = getUserConfirmation;
  }

  /**
   * 设置一个阻塞，传递一个提示消息
   * @param {*} block 可以是字符串，也可以一个函数，函数返回一个消息字符串
   */
  addBlock(block) {
    if (typeof block !== 'string' && typeof block !== 'function') {
      throw new TypeError('Block must be a string or function');
    }
    this._block = block;
    return () => {
      this._block = null;
    };
  }

  /**
   * 触发阻塞
   * @param {function} callback 当阻塞完成之后要做的事情（一般是跳转页面）
   */
  triggerBlock(location, action, callback) {
    if (!this._block) {
      callback();
      return;
    }
    let message; //阻塞消息
    if (typeof this._block === 'string') {
      message = this._block;
    } else {
      message = this._block(location, action);
    }
    //调用getUserConfirmation
    this.getUserConfirmation(message, (result) => {
      if (result === true) {
        //可以跳转了
        callback();
      }
    });
  }
}
```

## 核心模块 createBrowserHistory

```js
import ListenerManager from './ListenerManager';
import BlockManager from './BlockManager';

/**
 * 通过createBrowserHistory函数，返回一个history对象
 * @param {Object} options 配置对象
 * @returns history对象
 */
export default function createBrowserHistory(options = {}) {
  //为配置对象添加默认值
  const {
    basename = '',
    forceRefresh = false,
    keyLength = 6,
    getUserConfirmation = (message, callback) =>
      callback(window.confirm(message)),
  } = options;

  const listenerManager = new ListenerManager();
  const blockManager = new BlockManager(getUserConfirmation);

  function go(step) {
    window.history.go(step);
  }

  function goBack() {
    window.history.back();
  }

  function goForward() {
    window.history.forward();
  }

  /**
   * 根据配置路径参数和符加的信息跳转页面
   * @param {String or Object} path 跳转的路径
   * @param {String or Object} state 符加的信息
   */
  function push(path, state) {
    _changePath(path, state, true);
  }

  /**
   * 根据配置路径参数和符加的信息跳转页面
   * @param {String or Object} path 跳转的路径
   * @param {String or Object} state 符加的信息
   */
  function replace(path, state) {
    _changePath(path, state, false);
  }

  /**
   * 抽离的，可用于实现push或replace功能的方法
   * @param {*} path
   * @param {*} state
   * @param {*} isPush
   */
  function _changePath(path, state, isPush) {
    let action = 'PUSH';
    if (!isPush) {
      action = 'REPLACE';
    }
    const pathInfo = _pushHelper(path, state, basename);
    blockManager.triggerBlock(parsePathInfo(pathInfo, basename), action, () => {
      if (isPush) {
        window.history.pushState(
          { key: createKey(keyLength), state: pathInfo.state },
          null,
          pathInfo.path
        );
      } else {
        window.history.replaceState(
          { key: createKey(keyLength), state: pathInfo.state },
          null,
          pathInfo.path
        );
      }
      const location = createLocation(basename);
      listenerManager.triggerListener(location, history.action);
      history.location = location;
      history.action = action;
      if (forceRefresh) {
        window.location.reload();
      }
    });
  }

  function listen(listener) {
    return listenerManager.addListener(listener);
  }

  (() => {
    window.addEventListener('popstate', () => {
      const action = 'POP';
      const location = createLocation(basename);
      blockManager.triggerBlock(location, action, () => {
        listenerManager.triggerListener(location, action);
        history.action = action;
        history.location = location;
      });
    });
  })();

  function block(block) {
    return blockManager.addBlock(block);
  }

  function createHref(location) {
    const { pathname = '/', search = '', hash = '' } = location;
    return basename + pathname + search + hash;
  }

  const history = {
    action: 'POP',
    block,
    createHref,
    go,
    goBack,
    goForward,
    length: window.history.length,
    listen,
    location: createLocation(basename),
    push,
    replace,
  };

  return history;
}

/**
 * 根据path和state，得到一个统一的对象格式
 * @param {*} path
 * @param {*} state
 */
function _pushHelper(path, state, basename) {
  if (typeof path === 'string') {
    return {
      path,
      state,
    };
  } else if (typeof path === 'object') {
    //组装path
    let { pathname, search = '', hash = '', state = null } = path;
    search =
      search.charAt(0) !== '?' && search.length > 0 ? '?' + search : search;
    hash = hash.charAt(0) !== '#' && hash.length > 0 ? '#' + hash : hash;
    return {
      path: basename + pathname + search + hash,
      state,
    };
  } else {
    throw new TypeError('path must be string or object');
  }
}

/**
 * 返回一个location对象
 * @param {String} basename 配置的基路径
 * @returns
 */
function createLocation(basename) {
  //处理pathname
  let pathname = window.location.pathname.replace();
  const regExp = new RegExp(`^${basename}`);
  pathname = pathname.replace(regExp, '');
  //处理search
  const search = window.location.search;
  //处理hash
  const hash = window.location.hash;
  //处理state
  const windowHistoryState = window.history.state;
  const location = {
    pathname,
    search,
    hash,
  };
  let state;
  if (windowHistoryState === null) {
    state = undefined;
  } else {
    if (typeof windowHistoryState === 'string') {
      state = windowHistoryState;
    } else if (typeof windowHistoryState === 'object') {
      if ('key' in windowHistoryState) {
        location.key = windowHistoryState.key;
        state = windowHistoryState.state;
      } else {
        state = windowHistoryState;
      }
    }
  }
  location.state = state;

  return location;
}

/**
 * 根据路径信息返回一个location对象 路径信息例如{path:"/news/red?page=1&limit=10#abc",state:'123'}
 * @param {*} pathInfo
 */
export function parsePathInfo(pathInfo, basename) {
  // const regExp = new RegExp('^/.*(?=\\?)?')
  // const pathname = regExp.exec(pathInfo.path)
  // console.log(pathname);
  const { path } = pathInfo;
  let pathname, search, hash, state;
  const questionMarkIndex = path.indexOf('?');
  const sharpIndex = path.indexOf('#');
  if (questionMarkIndex === -1 && sharpIndex === -1) {
    pathname = path;
  } else if (questionMarkIndex !== -1 && sharpIndex === -1) {
    pathname = path.substring(0, questionMarkIndex);
    search = path.substring(questionMarkIndex);
  } else if (questionMarkIndex === -1 && sharpIndex !== -1) {
    pathname = path.substring(0, sharpIndex);
    hash = path.substring(sharpIndex);
  } else {
    if (questionMarkIndex > sharpIndex) {
      pathname = path.substring(0, sharpIndex);
      hash = path.substring(sharpIndex);
    } else {
      pathname = path.substring(0, questionMarkIndex);
      search = path.substring(questionMarkIndex, sharpIndex);
      hash = path.substring(sharpIndex);
    }
  }
  state = pathInfo.state;
  const regExp = new RegExp(`^${basename}`);
  pathname = pathname.replace(regExp, '');
  return {
    pathname,
    search,
    hash,
    state,
  };
}

function createKey(keyLength) {
  const key = Math.random()
    .toString(36)
    .substring(2, keyLength + 2);
  return key;
}

window.myHistory = createBrowserHistory({
  basename: '/news',
});

```



