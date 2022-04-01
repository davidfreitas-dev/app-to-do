<template>
    <div class="modal-save modal-confirm animate__animated animate__fadeIn" v-if="viewModal">
        <div class="modal-content animate__animated animate__bounceInDown">
            <span class="close" @click="viewModal = false">&times;</span>
            <h4>{{ message }}</h4>
            <input type="text" v-model="listName">
            <div class="modal-actions">
                <button class="confirm" @click="handleSave">Confirmar</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            listName: null,
            viewModal: false,
            message: 'Como deseja chamar esta lista?'
        }
    },
    methods: {
        showModal() {
            this.viewModal = true
        },
        handleSave() {
            this.$emit('handleSave', this.listName)
            Object.assign(this.$data, this.$options.data())
        },
    }
}
</script>

<style scoped>
/* The Modal (background) */
.modal-save {
    position: fixed; /* Stay in place */
    z-index: 1; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0,0,0); /* Fallback color */
    background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}
/* Modal Content/Box */
.modal-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
    color: var(--font);
    align-items: center;
    text-align: center;
    background-color: var(--bg);
    margin: 25% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid var(--bg);
    border-radius: 7px;
    width: 80%; /* Could be more or less, depending on screen size */
}

.modal-content h4 {
    margin-top: 1rem;
}

.modal-actions {
    display: flex;
    justify-content: center;
    align-items: center;
}

input {
    width: 90%;
    height: 45px;
    padding: 0 15px;
    margin-top: .75rem;
    color: var(--font);
    font-size: 1rem;
    letter-spacing: .75px;
    outline: none;
    border: 1px solid var(--secondary);
    border-radius: 5px;
    background-color: var(--light);
}

.confirm {
    outline: none;
    border: none;
    color: #fff;
    margin: 1rem .25rem;
    padding: .75rem 1.3rem;
    font-weight: bold;
    text-transform: uppercase;
    border-radius: 7px;
    background-color: var(--main);
    cursor: pointer;
}

.cancel {
    outline: none;
    border: none;
    color: #fff;
    margin: 1rem .25rem;
    padding: .75rem 1.3rem;
    text-transform: uppercase;
    border-radius: 7px;
    background-color: gray;
    cursor: pointer;
}

.close {
    position: relative;
    color: #aaa;
    font-size: 28px;
    font-weight: bold;
    margin-top: -15px;
    margin-right: -3px;
    align-self: flex-end;
}
.close:hover,
.close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
}

@media only screen and (min-width: 768px) {			
    .modal-content {
        width: 35%;
        margin: 10% auto; /* 15% from the top and centered */
    }
}

@media only screen and (min-width: 960px) {			
    .modal-content {
        width: 25%;
    }
}
</style>