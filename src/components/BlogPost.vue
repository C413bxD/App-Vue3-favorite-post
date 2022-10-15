<script setup>
// defineProps(["title","id","body"])
defineProps({
    title:String,
    id:Number,
    body: {
        type:String,
        default:"Sin descripcion"
    }
})
const emit = defineEmits(["CambiarFavorito"])
</script>
<template>
    <div class="card">
        <h5 class="card-title">
            {{id}} - {{title}}
        </h5>
        <div class="card-body">
            <p >{{body}}</p>
            <button @click="emit('cambiarFavorito',title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>
