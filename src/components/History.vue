<template>
    <div>
        <button
            type="button" 
            id="history_btn"
            data-bs-toggle="modal" 
            data-bs-target="#historyModal"
            class="d-flex justify-content-center align-items-center btn btn-lg rounded-circle position-fixed m-0" 
        >
            <ion-icon v-pre name="time-outline" class="icon"></ion-icon>
        </button>

        <div 
            tabindex="-1" 
            id="historyModal" 
            class="modal fade" 
            aria-hidden="true"
            aria-labelledby="historyModalLabel" 
        >
            <div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="historyModalLabel">
                            History
                        </h1>
                        <button 
                            type="button" 
                            class="btn-close" 
                            data-bs-dismiss="modal" 
                            aria-label="Close"
                        ></button>
                    </div>
                    <div class="modal-body">
                        <ul class="list-group">
                            <li 
                                :key="index" 
                                v-for="(item, index) in history" 
                                class="list-group-item d-flex justify-content-between align-items-center"
                            >
                                <div>
                                    <span class="fw-bold">
                                        {{ item.time }} - 
                                    </span> 
                                    {{ item.expression }}
                                </div>
                                <button 
                                    @click="$emit('restore', item.expression)" 
                                    data-bs-dismiss="modal"
                                    class="btn btn-primary btn-sm"
                                >
                                    <ion-icon name="open-outline"></ion-icon>
                                </button>
                            </li>
                        </ul>
                        <p 
                            v-if="history.length === 0" 
                            class="alert text-muted text-center mt-3"
                        >
                            No history :(
                        </p>
                    </div>

                    <div class="modal-footer">
                        <button 
                            type="button" 
                            class="btn btn-secondary" 
                            data-bs-dismiss="modal"
                        >
                            Close
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "History",
    props: {
        history: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
#history_btn {
    top: 15px;
    right: 0px;
    opacity: 0.8;
    transition: 0.3s;
    color: var(--text-color);
}
#history_btn:hover {
    opacity: 1;
    color: var(--text-color);
}
.icon {
    font-size: 1.5rem;
}

.modal-content,
.list-group,
.list-group-item,
.alert {
    color: var(--text-color);
    background-color: var(--btn-bg-color);
}
</style>