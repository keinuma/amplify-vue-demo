<template>
  <div>
    <el-row>
      <el-col>
        <el-form ref="postData" :model="postData" label-width="100px">
          <el-form-item label="Author">
            <el-input
                class="post-input"
                v-model="postData.author"
                placeholder="post"
                autosize
            ></el-input>
          </el-form-item>
          <el-form-item label="Content">
            <el-input
                class="post-input"
                type="textarea"
                rows="10"
                v-model="postData.content"
                placeholder="xxx"
                autosize
            ></el-input>
          </el-form-item>
        </el-form>
      </el-col>
    </el-row>
    <el-row>
      <el-col>
      <el-button @click="createPost">
        作成
      </el-button>
      </el-col>
    </el-row>
    <el-row>
      <el-card v-if="myPost">
        <div slot="header" class="clearfix">
          <span>Created Post</span>
        </div>
        {{ myPost }}
      </el-card>
    </el-row>
  </div>
</template>

<script>
import { API, graphqlOperation } from 'aws-amplify'
import * as mutaions from '@/graphql/mutations'

export default {
  name: 'CreatePost',
  data: function() {
    return {
      postData: {
        author: '',
        content: ''
      },
      myPost: ''
    }
  },
  methods: {
    createPost: function () {
      API.graphql(graphqlOperation(mutaions.createPost, this.postData ))
        .then((response) => {
          console.log(response)
          this.myPost = response
        })
        .catch((err) => {
          console.log(err)
        })
    }
  }
}
</script>

<style scoped>
</style>
