<template>
  <div id="home">
    <v-row justify="center" class="pt-10">
      <h1 class="display-2 font-weight-bold mb-3">
        Welcome!!
      </h1>
    </v-row>
    <v-row justify="center" class="pt-10">
      <v-card class="d-md-flex pa-5" outlined tile style="width: 900px;">
        <v-flex mb-3 xs12>
          <h2 class="headline font-weight-bold mb-3">
            Please upload the design document
          </h2>
          <v-file-input
            v-model="targetFile"
            label="File input"
            outlined
            dense
            counter
            show-size
            @change="setFile"
            class="pt-5"
          ></v-file-input>
          <v-row justify="center">
            <v-btn
              large
              color="primary"
              v-bind:disabled="isButtonDisabled"
              @click="submitFile"
            >
              Start review
            </v-btn>
          </v-row>
        </v-flex>
      </v-card>
    </v-row>
    <v-overlay :value="loading" opacity="0.95">
      <v-row>
        <v-progress-circular :size="135" :width="5" color="blue" indeterminate>
          now reviewing...
        </v-progress-circular>
      </v-row>
      <v-row justify="center" class="pt-5">
        <a href="#" @click.prevent.stop="loading = false">cancel</a>
      </v-row>
    </v-overlay>
    <v-dialog v-model="isShowResult" persistent width="600">
      <v-card>
        <v-card-title class="headline">Result</v-card-title>
        <v-card-text>
          <v-simple-table :height="450">
            <template v-slot:default>
              <thead>
                <tr>
                  <th class="text-left"></th>
                  <th class="text-left">指摘内容</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="item in result" :key="item.name">
                  <td>{{ item.name }}</td>
                  <td>{{ item.confirm }}</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="green darken-1" text @click="isShowResult = false"
            >Checked</v-btn
          >
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'

@Component
export default class HelloWorld extends Vue {
  isShowResult: boolean = false
  targetFile: any = null
  isButtonDisabled: boolean = true
  loading: boolean = false
  result: any[] = [
    { name: '指摘1', confirm: '脱字' },
    { name: '指摘2', confirm: '誤字' },
    { name: '指摘3', confirm: '不正' },
    { name: '指摘4', confirm: '脱字' },
    { name: '指摘5', confirm: '不正' },
    { name: '指摘6', confirm: '誤字' },
    { name: '指摘7', confirm: '脱字' },
    { name: '指摘8', confirm: '脱字' }
  ]

  setFile(event: any) {
    if (this.targetFile === undefined || this.targetFile === null) {
      this.isButtonDisabled = true
    } else {
      this.isButtonDisabled = false
    }
  }

  submitFile() {
    this.loading = true
    setTimeout(this.resultSet, 3000)
  }

  resultSet() {
    this.loading = false
    this.isShowResult = true
  }
}
</script>
