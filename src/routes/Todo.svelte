<script>

     let todoItem = '';
     let todoList = [];

     function add() {
          if (todoItem == '') {
               return;
          }
          todoList = [...todoList, {
               text: todoItem,
               done: false
          }]
          todoItem = '';
     }     

     function removeThis(index) {
          todoList.splice(index, 1);
          todoList = todoList;
     }
     function clearDone() {
          todoList = todoList.filter(t => !t.done);
     }
     function clearAll() {
          todoList = [];
     }
</script>

<form on:submit|preventDefault={add}>
     <input class="addtolist" bind:value={todoItem} type="text" autofocus/><button type="submit">Add</button>
</form>

<ul>
     {#each todoList as item, index}
          <li>
               <input type="checkbox" bind:checked={item.done}>
               <span class:done={item.done}>{item.text}</span>
               <span on:click={() => removeThis(index)} on:keypress={() => removeThis(index)} class="remove"></span>
          </li>
     {/each}
</ul>

{#if todoList.length > 0}
<button on:click={clearDone}>Clear Done</button>
<button on:click={clearAll}>Clear All</button>
{/if}

<style>
     ul {
          list-style: none;
     }
     .addtolist {
          padding: 0.75em;
     }
     .done {
          text-decoration: line-through;
          color: lightgray;
     }
     .remove {
          height: 1rem;
          width: 1rem;
          display: inline-block;
          background: url('./images/trash-bin.png') no-repeat;
          background-size: 100% auto;
          cursor: pointer;
     }
     button {
          border: none;
          padding: 0.75em;
          background-color: rgb(89, 89, 192);
          color: white;
          font-weight: bold;
          border-radius: 4px;
          cursor: pointer;
     }
     button:hover {
          background-color: rgb(116, 116, 226);
     }
</style>