

目的：当调用effect，需要返回fn，以及fn的返回值


```js
	it("should return runner when call effect", () => {

		let foo = 10;
		
		const runner = effect(() => {
		
		foo++;
		
		return "foo";
		
		});
		
		expect(foo).toBe(11);
		
		const r = runner();
		
		expect(foo).toBe(12);
		
		expect(r).toBe("foo");

});



```