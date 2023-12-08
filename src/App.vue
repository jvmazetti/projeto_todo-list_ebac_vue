<script setup>

    import { reactive } from 'vue';
    import Cabecalho from './components/Cabecalho.vue';
    import Formulario from './components/Formulario.vue';
    import ListaDeTarefas from './components/ListaDeTarefas.vue';

    const estado = reactive({
        filtro: 'todas',
        tarefaTemporaria:' ',
        tarefas: [
            {
                titulo: 'Estudar ES6',
                finalizada: false,
            },
            {
                titulo: 'Estudar SASS',
                finalizada: false,
            },
            {
                titulo: 'Ir para academia',
                finalizada: true,
            }
        ]
    })

    const getTarefaPendentes = () => {
        return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
    }

    const getTarefaFinalizadas = () => {
        return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
    }

    const getTarefasFiltradas = () => {
        const filtro = estado.filtro;
        switch (filtro) {
            case 'pendentes':
                return getTarefaPendentes();
            case 'finalizadas':
                return getTarefaFinalizadas();
            default:
                return estado.tarefas;
        }
    }

    const cadastrarTarefa = (e) =>{
        e.preventDefault()
        const tarefaNova = {
            titulo: estado.tarefaTemporaria,
            finalizada: false
        }
        estado.tarefas.push(tarefaNova);
        estado.tarefaTemporaria =' ';
    }
</script>

<template>
    <div class="container">
        <Cabecalho :tarefas-pendentes="getTarefaPendentes().length"/>
        <Formulario :trocar-filtro="evento => estado.filtro = evento.target.value" :tarefa-temporaria="estado.tarefaTemporaria" :edita-tarefa-temporaria="evento => estado.tarefaTemporaria = evento.target.value" :cadastrar-tarefa="cadastrarTarefa"/>
        <ListaDeTarefas :tarefas="getTarefasFiltradas()"/>
    </div>
</template>


