<script setup>


const props = defineProps(['cadastraTarefa', 'tarefaTemporari', 'trocarFiltro', 'editaTarefaTemp'])





</script>


<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporari" @change="props.editaTarefaTemp" required type="text"
                    placeholder="Digite aqui a Descricao da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>