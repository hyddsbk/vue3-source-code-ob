effect 是个底层 api 文档中看不到 

效果其实和 watchEffect 很类似 

effect(fn=>fn())
通过分析：fn 传入effect中需要立即执行fn, 为方便管理effect,实例类管理effect

```js
class ReactiveEffect(){
	private _fn: any;
	constructor(fn){
		this._fn = fn;
	}
	run(){
		this._fn();
	}
}



export const effect = (fn)=>{
	const _effect = new ReactiveEffect(fn)
	_effect.run()
}
	
```