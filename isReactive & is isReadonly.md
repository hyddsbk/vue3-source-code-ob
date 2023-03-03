如何实现是不是一个响应式对象?

假如是响应式对象,一定会走new proxy代理，所以可以利用这个特点来展开

``` js
	// 为何需要用！！
	// 假如value是响应式对象，那么获取值必定触发get操作
	export const isReactive = (value) =>{
		return !!value[ReactiveFlag["IS_REACTIVE"]]
	}
	
	new Proxy(raw, {
		get(target,key){
			if(key === 'IS_REACTIVE'){
				return true
			}

			const res = Reflect.get(target,key);
			return res
		}
	})
```