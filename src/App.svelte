<script>
	let tarefas = [];
	let novaTarefa = '';
  
	function adicionarTarefa() {
	  if (novaTarefa !== '') {
		tarefas = [...tarefas, { id: tarefas.length + 1, nome: novaTarefa, concluida: false }];
		novaTarefa = '';
	  }
	}
  
	function removerTarefa(id) {
	  tarefas = tarefas.filter(tarefa => tarefa.id !== id);
	}
  
	function alternarTarefa(id) {
	  tarefas = tarefas.map(tarefa =>
		tarefa.id === id ? { ...tarefa, concluida: !tarefa.concluida } : tarefa
	  );
	}
  </script>
  
  <div>
	<input class="input-field" bind:value={novaTarefa} placeholder="Adicionar nova tarefa" />
	<button class="button" on:click={adicionarTarefa}>Adicionar Tarefa</button>
  </div>
  
  <ul>
	{#each tarefas as tarefa (tarefa.id)}
	  <li>
		<input type="checkbox" bind:checked={tarefa.concluida} on:change={() => alternarTarefa(tarefa.id)} />
		<span style="text-decoration: {tarefa.concluida ? 'line-through' : 'none'}">{tarefa.nome}</span>
		<button class="button" on:click={() => removerTarefa(tarefa.id)}>Remover</button>
	  </li>
	{/each}
  </ul>