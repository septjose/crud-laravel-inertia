<script>
export default {
    name: 'ProjectDetail',
}
</script>

<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import { router } from '@inertiajs/vue3'
import { Link } from '@inertiajs/vue3'

defineProps({
    project: {
        type: Object,
        required: true,
    },
})
const deleteProject = id => {
    if (confirm('¿Estás seguro de querer eliminar este proyecto?')) {
        router.delete(route('projects.destroy', id))
    }
}
</script>

<template>
    <AppLayout title="Detalle proyecto">
        <template #header>
            <h1 class="font-semibold text-xl text-gray-800 leading-tight">
                Detalle proyecto
            </h1>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <h1 class="text-2xl font-bold mb-4">{{ project.name }}</h1>
                        <p class="text-gray-700 mb-4">
                            Autor: {{ project.user.name }}
                        </p>
                        <p class="text-gray-700 mb-4">{{ project.description }}</p>
                        <p class="text-gray-700">{{ project.created_at }}</p>
                    </div>
                </div>
            </div>

            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8 mt-4">
                <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <Link :href="route('projects.index')" class="bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded">Volver</Link>
                        <Link :href="route('projects.edit', project.id)" class="ml-2 bg-indigo-500 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded">Editar</Link>
                        <Link
                            class="ml-2 bg-indigo-500 hover:bg-indigo-700 text-white font-bold py-2 px-4 rounded"
                            @click="deleteProject(project.id)"
                        >
                            Eliminar
                        </Link>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
