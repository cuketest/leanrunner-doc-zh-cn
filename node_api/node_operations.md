# 对象操作API

对象操作API的方法分为两类，操作和属性。操作对控件做实际的操作，属性是获得控件的实际属性。因为是异步的，所以获取属性也是以方法的形式，即调用时需要加上括号”\(\)”，并且返回的是Promise。在`async`函数中可通过加`await`获得实际的值。

## 共有的API

不同类型的对象操作有不同的操作和属性。它们都有一些共用的操作和属性，如下：

```javascript
export interface IWinControl extends IWinContainer {
  click(x?: number, y?: number, mousekey?: number): Promise<void>;
  dblClick(x?: number, y?: number, mousekey?: number): Promise<void>;
  wheel(value: number): Promise<void>;
  exists(time: number): Promise<boolean>;
  hScroll(value: any): Promise<void>;
  vScroll(value: any): Promise<void>;
  getProperty(propertyIds: PropertyIds): Promise<string | boolean | number>;
  waitProperty(propertyIds: PropertyIds, value: string, timeoutSeconds: number): Promise<boolean>
  drop(x?: number, y?: number): Promise<void>;
  drag(x?: number, y?: number): Promise<void>;
  pressKeys(keys: string): Promise<void>;
  takeScreenshot(filePath: string): Promise<void>;

//properties
  text(): Promise<string>;
  name(): Promise<string>;
  hwnd(): Promise<number>;
  x(): Promise<number>;
  y(): Promise<number>;
  height(): Promise<number>;
  width(): Promise<number>;
  enabled(): Promise<boolean>;
  focused(): Promise<boolean>;
  helpText(): Promise<string>;
  labeledText(): Promise<string>;
  value(): Promise<string>;
  processId(): Promise<number>;
  modelImage(options?: {encoding: 'buffer' | 'base64'}): Promise<string>  //base64 is the default
}
```

具体每个操作和属性的帮助可以在模型管理器中找到。

## 每个对象自己的API

其它的对象因为是继承IWinControl，所以除了这些操作和属性外，还有一些其它的操作和属性。例如：

CheckBox控件有一个操作，`check`用于设置是勾选还是清除勾选，一个属性`checked`用于判断CheckBox的勾选状态：

```javascript
export interface IWinCheckBox extends IWinControl {
  check(value: boolean): Promise<void>;
  checked(): Promise<boolean>;
}
```

下面是ComboBox特有的方法和属性：

```javascript
export interface IWinComboBox extends IWinControl {
  getItem(index: number): Promise<string>;
  itemCount(): Promise<number>;
  selectedItem(): Promise<string>;
  select(value: string | number): Promise<void>;
  open(): void;
}
```

更多的控件的操作和属性的帮助可以在模型管理器中找到。

## 虚拟控件API

虚拟控件是特殊的控件，因此它的操作不同于其它控件。它没有其它Windows控件共有的操作和属性，它只有下面的操作 和属性。

```javascript
export interface IWinVirtual {
  click(x: number, y: number, mousekey: number): Promise<void>;
  pressKeys(keys: string): Promise<void>;
  wheel(value: number): Promise<void>;
}
```

