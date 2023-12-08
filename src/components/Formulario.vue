<script setup>
    const props = defineProps(['cadastrarTarefa', 'tarefaTemporaria', 'trocarFiltro', 'editaTarefaTemporaria' ])
</script>


<template>
     <form @submit="props.cadastrarTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria" @change="props.editaTarefaTemporaria" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control"/>
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>
