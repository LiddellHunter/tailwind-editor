<script>
	
	import List from './List.svelte'
	let klass = ''
	export let open = false
	export {klass as class}
	export let selected
	
    const getWindow = () => {
        if(window) return window;
    }
	$: posKlass = lNode?.getBoundingClientRect()?.bottom > getWindow().__edw.innerHeight ? 'bottom-0 mb-8' : '' 

	let lNode


	export let list = [
		{
			label:'none',
			value:'none'
		},
		{
			label:'tight',
			value:'tight'
		},
		{
			label:'snug',
			value:'snug'
		},
		{
			label:'normal',
			value:'normal'
		},
		{
			label:'relaxed',
			value:'relaxed'
		},
		{
			label:'loose',
			value:'loose'
		}
	]

	function toggleList(e){
		open= !open
		e.preventDefault()
		e.stopPropagation()
	}
	
	function hideList(){
		open = false
	}
	if(window)
	    window.__edw.addEventListener('click', hideList)
</script>

<div class="relative">
	<div class="cursor-pointer flex h-full" on:click={toggleList}>
		<slot>Click To show</slot>
	</div>
	{#if open}
	<div class="absolute -ml-1 z-920 z-20 {klass} {posKlass}" bind:this={lNode}>
		<List {list} {selected} on:select />
	</div>
	{/if}
</div>