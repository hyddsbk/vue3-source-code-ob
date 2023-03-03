vue3响应式原理，通过 new  proxy代理对象以及Reflect 反射来对源对象进行操作
Reflect

思考：
[[如何收集依赖？]]
[[如何触发依赖？]]

代码实现：

```js

export const reactive = (raw) => {
	return new Proxy(raw, {
		get(target,key){
			const res = Reflect(target,key);
			// TODO 收集依赖 
			track(target,key);
			return res		
		},
		set(target,key,value){
			const res = Reflect(target,key,value);
			// TODO 触发依赖
			trigger(target,key);
			return res
		}
	})
}

```

- [[调用effect返回调用的函数]]
- [[scheduler 实现]]
- [[stop]]
- [[readonly]]
- [[isReactive & is isReadonly]]
- [[实现 reactive & readonly 嵌套功能]]
- [[实现 shallowReadonly]]
