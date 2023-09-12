<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <form @submit.prevent="tambahkan">
    <div>
      <div class='item' v-for="(todoList, index) in listText" :key="index"> 
        <div class='content' v-if="! todoList.edit">{{index+ 1 + ". "}}{{ todoList.text }}</div>
        <!-- <div class="indexText">
          {{index+ 1 + ". "}}
        </div>
        <div class="text">
          <input v-model="editText" type="text" class="field-value form-control" @blur="blurField">
        </div> -->
        <div class="indexText" v-else >{{index+ 1 + ". "}}
          <input class="editText" type="text" v-model="todoList.text" :ref="'task'">
        </div>
        <div class='action'><button @click="removeItem(index)">Hapus</button></div>
        <div class='action' v-if="! todoList.edit"><button @click="editItem(index)">Edit</button></div>
        <div class='action' v-else><button @click="disableEdit(index)">Edit</button></div>
      </div>
    </div>
      <input class="inputTodo" type="text" v-model='inputText'/> <button @click="tambahkan">Tambahkan</button>
      <p>{{todoMore}}</p>
    </form>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
        return {
            inputText: '',
            listText: [],
            todoMore:'',
        }
    },
  methods:{
    tambahkan(){
      const trimmedText = this.inputText.trim()
      if(trimmedText)
      {
          this.listText.push({
              text: trimmedText,
              edit: false
          })
          this.inputText = '';
          if(this.listText.length >= 4)
          {
              this.todoMore = 'Hebat!';
          }
          else if(this.listText.length < 4)
          {
            this.todoMore = '';
          }
      }
    },
    removeItem: function(index) {
      this.listText.splice(index, 1);
    },
    editItem: function(index) {
      //return (this.inputText[inputText] == '' || this.inputText == inputText)
      this.listText[index].edit = true;
      this.$nextTick(() => {
        let input = this.$refs.task[0];
        input.focus();
      });
    },
    disableEdit: function(index) {
      this.listText[index].edit = false;
    },
  }
}
</script>

<style>
.inputTodo, .ediText{
    width: 80%;
}
.content{
    width: 80%;
    display: flex;
}
.action{
    width: 50px;
    text-align: center;
    padding: 4px 8px;
}
.item{
    display: flex;
    padding: 4px 8px;
    margin: 12px 0;
}
</style>
