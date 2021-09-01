<template>
  <div class="container col-sm-8">
    <h2 class="text-center mt-5 ">Aplikasi Todolist</h2>
  
    <div class="d-flex mt-5 ">
      <input v-model="task" type="text" placeholder="Tambahkan Kegiatan" class="form-control" >
      <button @click="menambahKegiatan" class="btn btn-warning text-light ">Submit</button>
    </div>

      <table class="table table-bordered mt-5">
        <thead class="text-center">
          <tr>
            <th  scope="col" class="col-md-1">No</th>
            <th  scope="col" class="col-md-5">Task</th>
            <th  scope="col" class="col-md-2">Status</th>
            <th  scope="col" class="col-md-1">Edit</th>
            <th  scope="col" class="col-md-1">Delete</th>
           </tr>
        </thead>
        <tbody>
          <tr v-for="(giat, index) in kegiatan" :key="index">
            <td class="text-center">{{ giat.no }}</td>
            <td>
              <span :class="{'Selesai': giat.status === 'Selesai'}">
              {{ giat.nama }}
              </span>
            </td>
            <td class="text-center">
              <span @click="ubahstatus(index)" class="pointer">
                {{ giat.status }}
              </span>
            </td>
            <td class="text-center">
              <div @click="editKegiatan(index)">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td class="text-center" @click="HapusKegiatan(index)">
              <div>
                <span class="fa fa-trash"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      
      
  </div>
 
 


  

</template>

<script>
export default {
  data() {
    return {
      task: '',
      editedKegiatan: null,
      statusaktif: ['Melakukan','Sedang Dikerjakan','Selesai'],
      kegiatan: [
        {
          no     : 1,
          nama   : 'Belajar PHP',
          status : 'Melakukan'
        },
        {
          no     : 2,
          nama   : 'Belajar Vue',
          status : 'Sedang dikerjakan'  
        },
      ] 
  }
  },
  methods: {

    menambahKegiatan(){
    if(this.task.length === 0 ) return;

    if(this.editedKegiatan === null){
      this.kegiatan.push({
        no     : this.kegiatan.length+1,
        nama   : this.task,
        status : 'Melakukan'
        });
    } else{
        this.kegiatan[this.editedKegiatan].nama = this.task;
        this.editedKegiatan=null;
      }
      this.tasks = '';
    },
    
    HapusKegiatan(index){
      if(index < this.kegiatan.length & index > 0){
        this.tasks = this.kegiatan.splice(index, 1);
      }
    
    },

    editKegiatan(index){
    this.tasks=this.kegiatan[index].nama ;
    this.editedKegiatan= index;  
    },

    ubahstatus(index){
      let newIndex = this.statusaktif.indexOf(this.kegiatan[index].status);
      if(++newIndex>2) newIndex = 0;
      this.kegiatan[index].status = this.statusaktif[newIndex];
    }
  }
}
</script>
<style scoped>
  .pointer{
    cursor: pointer;
  }
  .Selesai{
    text-decoration: line-through;
  }
</style>





