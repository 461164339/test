
// 第一题
// 根据输入的数组中每项的 before/after/first/last 规则，输出一个新排好序的数组或者链表。
// 要求，多解的情况可以只求一解，如果无解要求程序能检测出来。
// 注意输入数组是无序的，before 和 after
// 规则不需要紧邻着指定的元素，只要满足是 before/after 即可。

const arr = [
  { id: 1 },
  { id: 2, before: 1 }, // 这里 before 的意思是自己要排在 id 为 1 的元素前面
  { id: 3, after: 1 }, // 这里 after 的意思是自己要排在 id 为 1 元素后面
  { id: 5, first: true },
  { id: 6, last: true },
  { id: 7, after: 8 }, // 这里 after 的意思是自己要排在 id 为 8 元素后面
  { id: 8 },
  { id: 9 },
];

function transformData(arr) {
  function sortArray(res) {
    let first = res.findIndex((item) => item.first);
    let last = res.findIndex((item) => item.last);
    res.unshift(res[first]);
    res.splice(first + 1, 1);
    res.push(res[last]);
    res.splice(last, 1);
  }

  let res = arr.sort((a, b) => a.id - b.id);
  sortArray(res);

  for (let i = 0; i < res.length; i++) {
    if (res[i].before) {
      let beforeIndex = res.findIndex((item) => item.id === res[i].before);
      res.splice(beforeIndex - 1, 0, res[i]);
      res.splice(i + 1, 1);
    }
  }

  for (let j = 0; j < res.length; j++) {
    if (res[j].after) {
      let afterIndex = res.findIndex((item) => item.id === res[j].after);
      let tempData = res[j];
      res.splice(j, 1);
      res.splice(afterIndex + 1, 0, tempData);
    }
  }

  sortArray(res);

  return res;
}

console.log(transformData(arr));

// 第二题
// 将输入的数组组装成一颗树状的数据结构，时间复杂度越小越好。要求程序具有侦测错误输入的能力。注意输入数组是无序的。

const Input = [
  { id: 1, name: "i1" },
  { id: 2, name: "i2", parentId: 1 },
  { id: 4, name: "i4", parentId: 3 },
  { id: 3, name: "i3", parentId: 2 },
  { id: 8, name: "i8", parentId: 7 },
];

function array2Tree(arr) {
  if (!Array.isArray(arr) || !arr.length) return;
  let map = {};
  arr.forEach((item) => (map[item.id] = item));

  let roots = [];
  arr.forEach((item) => {
    const parent = map[item.parentId];
    if (parent) {
      (parent.children || (parent.children = [])).push(item);
    } else {
      roots.push(item);
    }
  });

  return roots;
}
console.log(array2Tree(Input));

// 第三题
// 设计事件总线
class EventEmitter {
  listeners = {};
  on(event, listener) {
    if (this.listeners[event]) {
      this.listeners[event].push(listener);
    } else {
      this.listeners[event] = [listener];
    }
  }
  emit(event, params) {
    if (!this.listeners[event]) return;
    this.listeners[event].forEach((listener) => {
      listener(params);
    });
  }
  addEventListener(event, listener) {
    this.on(event, listener);
  }
  removeAllListeners(event) {
    if (!this.listeners[event]) return;
    delete this.listeners[event];
  }
  removeListeners(event, listener) {
    if (!this.listeners[event]) return;
    const index = this.listeners[event].indexOf(listener);
    this.listeners[event].splice(index, 1);
  }
  once(event, listener) {
    this.on(event, () => {
      let args = Array.prototype.slice.call(arguments);
      listener.apply(null, args);
      this.removeListeners(event, listener);
    });
  }
}

const bus = new EventEmitter();

bus.on("message", function (text) {
  console.log("第一次监听");
  console.log(text);
});

const callback2 = function (text) {
  console.log("第二次监听");
  console.log(text);
};

bus.on("message", callback2);

bus.emit("message", "hello world 1");

bus.removeListeners("message", callback2);

bus.emit("message", "hello world 2");

bus.once("once", function (text) {
  console.log(text);
});
bus.emit("once", "test once 1");
bus.emit("once", "test once 2");
