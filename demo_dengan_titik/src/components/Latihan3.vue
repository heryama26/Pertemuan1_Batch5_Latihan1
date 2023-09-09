<template>
<div id="todo-list">
    <form @submit.prevent="tambahkan">
        <h1>My Todo List</h1>
        <p v-for="text in listText" :key="text.text" @click="tambahkan">{{ text.text }}</p>
        <input type="text" v-model='inputText'/> <button v-on:click="tambahkan">Tambahkan</button>
        <p>{{ todoMore }}</p>
    </form>
</div>
</template>

<script>
export default {
    name: 'Latihan-3',
    data() {
        return {
        inputText: '',
            listText: [{
                text:''
            }],
            todoMore:''
        }
    },
    methods:{
        tambahkan(){
            const trimmedText = this.inputText.trim()
            if(trimmedText)
            {
                this.listText.push({
                    text: trimmedText,
                })
                if(this.listText.length > 4)
                {
                    this.todoMore = 'Hebat!';
                }
                this.inputText = '';
            }
        }
    }
//     mounted() {
//     const hello = 'Hello World!'
//     debugger
//     this.text = hello
//   }
}
</script>