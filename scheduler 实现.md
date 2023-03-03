

实现scheduler单元测试

目的：effect传入的option:{ scheduler }
			- 初始化执行fn，scheduler不被调用
			- 再次触发会调用scheduler
			- 再次触发effect返回的fn，会执行fn

```js

	it("scheduler", () => {

		let dummy;
		
		let run: any;
		
		const scheduler = jest.fn(() => {
		
		run = runner;
		
		});
		
		const obj = reactive({ foo: 1 });
		
		const runner = effect(
		
		() => {
		
		dummy = obj.foo;
		
		},
		
		{ scheduler }
		
		);
		
		  
		
		expect(scheduler).not.toHaveBeenCalled();
		
		expect(dummy).toBe(1);
		
		  
		
		obj.foo++;
		
		expect(scheduler).toHaveBeenCalledTimes(1);
		
		expect(dummy).toBe(1);
		
		  
		
		run();
		
		expect(dummy).toBe(2);

});

```