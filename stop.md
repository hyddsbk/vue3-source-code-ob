
实现stop单元测试

目的：effect 返回的fn, 用stop调用返回的fn, 将清理掉容器中的effect，再次执行重新收集依赖，触发依赖。

```js
	// spec
	it("stop", () => {

		let dummy;
		
		const obj = reactive({ prop: 1 });
		
		const runner = effect(() => {
		
			dummy = obj.prop;
		
		});
		
		obj.prop = 2;
		
		expect(dummy).toBe(2);
	
		stop(runner);
		
		obj.prop = 3;
		
		expect(dummy).toBe(2);
		
		runner();
		
		expect(dummy).toBe(3);
		
	});
```