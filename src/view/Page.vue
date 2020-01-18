<template>
  <v-app id="inspire">
    <v-container fluid class="pa-0">
      <v-row align="center">
        <v-col cols="12" sm="12" md="12">
          <div class="text-center">
            <div class="my-2">
              <v-btn 
                @click="openDialog()"
                large 
                color="blue" 
                dark
              >
                <v-icon class="mr-2">cloud_upload</v-icon>
                Upload
              </v-btn>
            </div>
          </div>
        </v-col>
      </v-row>
    </v-container>
    <v-dialog v-model="dialog" persistent max-width="900px">
      <v-card>
        <v-card-title>
          <template>
            <v-icon style="margin-right:10px;" large color="#41B883" >cloud_upload</v-icon> 
            <span class="headline" large>파일 업로드</span>
          </template>
          <v-spacer></v-spacer>
          <v-btn icon @click="closeDialog()">
            <v-icon>clear</v-icon>
          </v-btn>
        </v-card-title>
        <v-card-text>
          <v-row>
            <v-col cols="12" sm="12" md="12" style="position: relative; border:1px solid #41B883; border-style:dashed; ">
              <div class="example-drag">
                <div v-show="$refs.upload && $refs.upload.dropActive" class="drop-active">
                  <h3>Drop files to upload</h3>
                </div>
                <template v-if="files.length">
                  <!-- {{files}} -->
                  <v-data-table 
                    dense 
                    :headers="headers" 
                    :items="files" 
                    item-key="name" 
                    class="elevation-1"
                    hide-default-footer
                  >
                  </v-data-table>
                  <v-btn
                    class="ma-2"
                    style="padding:0px;"
                    color="info"
                    @click="uploadStart()"
                  >
                    <v-icon style="margin-right:5px;">arrow_upward</v-icon>UpLoad Start
                  </v-btn>
                </template>
                <template v-else>
                  <FileUpload
                    class="btn btn-primary"
                    :multiple="true"
                    :drop="true"
                    :drop-directory="true"
                    v-model="files"
                    ref="upload"
                    @input="onDrop"
                  >
                  </FileUpload>
                  <v-row>
                    <v-col cols="12" sm="12" md="12">
                      <div class="text-center p-5">
                        <h4>Drop files anywhere to upload<br/>or</h4>
                          <v-btn
                            class="ma-2"
                            style="padding:0px;"
                            color="info"
                          >
                            <label for="file" style="padding:0px 8px;"><v-icon style="margin-right:5px;">add_circle</v-icon>Select Files</label>
                          </v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </template>
              </div>
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import FileUpload from 'vue-upload-component';

export default {
  components: {
    FileUpload
  },
  data: ()=> ({
    dialog: false,
    files: [],
      headers: [
        { text: 'name', value: 'name' },
        { text: 'size', value: 'size' },
      ],
  }),
  methods: {
    openDialog() {
      this.dialog = true;
    },
    closeDialog() {
      this.dialog = false;
    },
    onDrop(item){
      console.log(item)
    },
  }
}
</script>