<script lang="ts">
	
	import { LightSwitch } from '@skeletonlabs/skeleton';

	let todosList : todoType[] = [];
	let input :string = ""
	function saveTodo(i:number, isEditing: boolean) {
		todosList[i].isEditing = isEditing;
	}
	function editTodo(i:number, isEditing: boolean) {
		todosList[i].isEditing = isEditing;
	}
	function deleteTodo(i:number){
		todosList.splice(i,1)
		todosList=todosList
	}
	function addTodo (){
		todosList = [...todosList,{ todo: input, isEditing: false, done: false }]
	input = ""
	}
  
</script>
<LightSwitch />


<div class="container h-full mx-auto flex justify-center items-center">
	<div class=" text-center items-center">
		<h1>@UserName</h1>
		<img alt="user" src="/user.png"  >
		<h1>Bio of user </h1>
		<div>
			<form >
				<input class="text-blue-600" type="text" bind:value={input} />
				<button on:click={addTodo}>Add</button>
			</form>
		</div>
		<h1>Todo List</h1>
		{#each todosList as todo, i}
			<div class="flex">
				<input type="checkbox" bind:checked={todo.done} />

				<div class="flex flex-col">
					{#if todo.isEditing}
					<div class="flex items-center">
						<input
							type="text"
							class="block card card-hover p-4 text-blue-600"
							bind:value={todo.todo}
							class:done={todo.done}
							on:keydown={event => {
								if (event.key === 'Enter') {
								  saveTodo(i, false); 
								}}}
						/>
						<div class="flex flex-col">
							<button on:click={() => saveTodo(i, false)}> Save </button>
							<button on:click={()=>deleteTodo(i)}>X</button>
						</div>
						</div>
					{:else}
					<div class="flex items-center">
						<a  href={'https://' + todo.todo} target="_blank" class="block card card-hover p-4 text-blue-600" class:done={todo.done}>{todo.todo}</a>
						<div class="flex flex-col">
							<button on:click={() => editTodo(i, true)}> Edit </button>
							<button on:click={()=>deleteTodo(i)}>X</button>
						</div>
					</div>
					{/if}
				</div>
			</div>
		{/each}
	</div>
</div>

<style>
	.done{
		text-decoration:line-through;
	}
</style>