
<template>
  <div class="container py-5">
    <div class="row">
      <div class="border-right">
        <p class="lead">Ticket Details</p>
        <form action="">
          <!--Category-->
          <div class="form-group">
            <label for="category">Category</label>
            <div class="input-group">
               <select class="form-select" name="category" v-model="selectedCategories" multiple >
                <option v-for="cate in categories" :value='cate' :key="cate.value">
                  {{ cate.name }}
                </option>
              </select>
            </div>
          </div>
          <!--Type-->
          <div class="form-group col">
            <label for="">Type</label>
            <div class="input-group">
              <div class="input-group">
                 <select class="form-select" v-for="cate in selectedCategories" v-model="cate.selectedTypes"  :key="cate.name" multiple>
                  <option v-for="type in cate.types" :value="type" selected :key="type.name">{{type.name}}</option>
                </select>
              </div>
            </div>
          </div>
        <!--Subject Input-->
          <div class="form-group">
            <label for="subject">Subject</label>
            <input type="text" class="form-control"></input>
          </div>
          <!--Description-->
          <div class="form-group">
            <label for="description">Description</label>
            <input type="text" class="form-control"></input>
          </div>
          <!--Message-->
          <div class="form-group">
            <label for="message">Message</label>
            <textarea type="text" rows="7" class="form-control"></textarea>
          </div>
          <!--file upload-->
          <div class="form-group">
            <label for="">Ticket Files & Documents</label>
            <div>     
              <div class="line">
              <div class="up-cv">
                <div class="name-cv">
                  <h5 v-if="uploadedFileName">{{ uploadedFileName }}</h5>
                  <span
                    v-if="uploadedFileName"
                    class="material-symbols-outlined deleteBtn"
                    @click="deleteFile"
                  >
                    delete
                  </span>
                </div>
                <button
                  class="btn btn-outline-primary btn-lg"
                  @click="onFileChange"
                  type="button"
                  id="custom-button"
                >
                + Attach File
                </button>

                <input
                  id="real-file"
                  type="file"
                  style="display: none"
                  name="image"
                  @change="fileName"
                />
                
                </div>
              </div>
            </div>
          </div>

          <div class="form-group d-flex  position-absolute bottom-0 end-0">
            <button type="button" class="btn btn-light mx-1" >Cancel</button>
            <button type="button" class="btn btn-success mx-1" >Submit</button>
          </div>
        </form>
      </div>
    </div>
  </div>
  
</template>
<script>

export default {
 
  data() {
    const categories = [
  { 
    name: 'Hardware', 
    types: [
      {name: 'Laptop' },
      {name: 'Mobile' },
      {name: 'Peripherals' },
      {name: 'Desk Phone' },
      {name: 'Printers' },
      {name: 'Other' }
    ], 
    selectedTypes: [] },
  { 
    name: 'Software', 
    types: [
      { name: 'Teams/Zoom' },
      { name: 'Mobile BlackBerry' },
      { name: 'Adobe' },
      { name: 'Outlook' },
      { name: 'Microsoft Office' },
      { name: 'Other' }
    ], 
    selectedTypes: []},
  { 
    name: 'Network', 
    types: [
      { name: 'Network Access' },
      { name: 'Connectivity' },
      { name: 'VPN' },
      { name: 'Driver' },
      { name: 'Other' }
    ], 
    selectedTypes: [] 
  },
  { 
    name: 'In-Processing', 
    types:[
      { name: 'Access Badge' },
      { name: 'Common Access Card(CAC)' },
      { name: 'SIPR' },
      { name: 'Trello' },
    ], 
    selectedTypes: [] 
  }
    ]
    return {
      categories,
      selectedCategories: [],
      uploadedFileName: null
    };
    
  },
  methods: { 
        handleFileUpload: function () {
          this.file = this.$refs.file.files[0];
        },      
        chooseFiles: function() {
        document.getElementById("fileUpload").click()
        },
        onFileChange() {
          document.getElementById('real-file').click();
        },
        fileName(e) {
          this.uploadedFileName = e.target.value;
        },
        deleteFile() {
          this.uploadedFileName = null;
        },     
  }, 
  computed:{
    originalSelectedCategories(){
      return this.selectedCategories.map(cate => cate) 
    },
    originalSelectedTypes(){
      return this.selectedTypes.reduce((acc, cate) => {
        acc.push(cate.selectedTypes.map(type => type))
        return acc
      },[])
    }
  }
};

</script>

<style>
#custom-button {
  display: inline-block;
  border: 1px solid grey;
  padding: 10px;
  cursor: pointer;
 }
 #custom-button span {
  display: inline-block;
  vertical-align: bottom;
 }
 #app {
   font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
 }
.deleteBtn {
 cursor: pointer;
 color: red;
 }

</style>
