<template>
    <div class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center fade-in">
        <div class="bg-white rounded-lg p-6 max-w-md w-full relative">
            <button @click="$emit('close')" class="absolute top-2 right-2 text-gray-500">✕</button>
            <div class="modal-content">
                <slot></slot>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
export default {
    emits: ['close']
};
</script>

<style scoped>
.fade-in {
    animation: fadeIn 0.5s cubic-bezier(0.42, 0, 0.58, 1) both;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }

    to {
        opacity: 1;
    }
}

button {
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
}

.modal-content {
    /* Optional styles for modal content */
}
</style>
