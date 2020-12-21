<template>
  <div class="container" >
    <div class="col-12">
      <div class="card">
        <div class="card-header" align= "center">
          <strong>Yapılacaklar Listesi</strong>
        </div>
        <div class="card-body">
          <table class="table">
            <tbody v-if="items.length">
              <tr :key=index v-for="(item,index) in items">
                <td>
                    <p :class="{'done1': item.done}">{{item.title}}</p>
                </td>
                <td>
                  <div class="actions">
                        <button class="btn-picto" style="font-size:20px;color:green;border:none;" type="button" @click="changeStatus(index)">
                            <i aria-hidden="true" style="font-size:20px;color:green;border:none;" class="material-icons">{{item.done ? 'check_box' : 'check_box_outline_blank'}}</i>
                        </button>
                        <button class="btn-picto" type="button" aria-label="Delete" style="font-size:20px;color:red;border:none"  @click="removeItem(index)">
                            <i aria-hidden="true" class="material-icons" style="font-size:20px;color:#d63031;border:none">delete</i>
                        </button>
                    </div>
                </td>
              </tr>
            </tbody>
            <p class="text-danger" v-else align="center">Eklenmiş veri yok</p>
          </table>
          <hr/>
          <form class="form-group" @submit.prevent="addNewItem">
            <div class="input-group mb-3">
              <input type="text" class="form-control" placeholder="Yeni Ekle" aria-label="Yeni Ekle" aria-describedby="basic-addon2" v-model="newItemTitle">
              <div class="input-group-append">
                <button class="btn btn-outline-secondary" type="submit">Ekle</button>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data(){
    return{
      newItemTitle: '',
      items: [],
    }
  },
  methods:{
    addNewItem(){
      if(this.newItemTitle==''){
        return;
      }
      this.items.push({
        title:this.newItemTitle,
        done:false,
      })
      this.newItemTitle='';
    },
    removeItem(index){
      this.items.splice(index,1);
    },
    changeStatus(index){
      const item=this.items[index];
      item.done=!item.done;
    }
  }
}
</script>
<style>
    body{
      margin: 40px auto;
      list-style: none;
      text-decoration: none;
      box-sizing: border-box;
      -webkit-overflow-scrolling: touch;
      font-family: 'Poppins', sans-serif;
      font-size: 1.1rem;
    }
    .actions{
      float: right;
    }
    .done1{
      text-decoration:line-through;
      color: green;
    }
    form {
        margin-top: 3rem;
        display: flex;
        flex-wrap: wrap;
    }
    form label {
        min-width: 100%;
        margin-bottom: .5rem;
        font-size: 1.3rem;
    }
    form input {
        flex-grow: 1;
        border: none;
        background: #f7f1f1;
        padding: 0 1.5em;
        font-size: initial;
        height: 33px;
    }
    tr{
      background-color: #efefef;
    }
</style>