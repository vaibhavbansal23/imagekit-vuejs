/* eslint-disable no-console */
<template>
  <div class="sample-app">
    <h1>Hi! This is an ImageKit Vue SDK Demo!</h1>
    <p>Let's add an Image</p>
    <IKImage
      :publicKey="publicKey"
      :urlEndpoint="urlEndpoint"
      :src="src"
    />
    <p>Let's transform this once</p>
    <IKImage
      :publicKey="publicKey"
      :urlEndpoint="urlEndpoint"
      :src="src"
      :transformation="[{height:300,width:400}]"
    />
    <p>Let's transform this more than once</p>
    <IKImage
      :publicKey="publicKey"
      :urlEndpoint="urlEndpoint"
      :path="path"
      :transformation="[{height:300,width:400},{rotation:90}]"
    />

    <p>LQIP</p>
    <IKImage
      :publicKey="publicKey"
      :urlEndpoint="urlEndpoint"
      :src="src"
      :lqip="{active:true,threshold:20}"
    />

    <p>Adding a Image with Context</p>
    <IKContext :publicKey="publicKey" :urlEndpoint="urlEndpoint">
      <IKImage :path="path" :transformation="[{height:300,width:400}]" />
    </IKContext>
    <p>Upload</p>
    <IKContext
      :publicKey="publicKey"
      :urlEndpoint="urlEndpoint"
      :authenticationEndpoint="authenticationEndpoint"
    >
      <IKUpload fileName="new_file_1" :tags="['tag1','tag2']" :responseFields="['tags']" :onError="onError" :onSuccess = "onSuccess"/>
    </IKContext>
    <p>To use this funtionality please remember to setup the server</p>
  </div>
</template>

<script>
import { IKImage, IKContext, IKUpload } from "imagekitio-vue";

let urlEndpoint= process.env.VUE_APP_URL_ENDPOINT;
if(urlEndpoint[urlEndpoint.length-1] === "/")
    urlEndpoint = urlEndpoint.slice(0,urlEndpoint.length-1);

let path = "/default-image.jpg";

export default {
  name: "app",
  components: {
    IKImage,
    IKContext,
    IKUpload
  },
  data() {
    return {
      urlEndpoint: urlEndpoint,
      publicKey: process.env.VUE_APP_PUBLIC_KEY,
      authenticationEndpoint: process.env.VUE_APP_AUTHENTICATION_ENDPOINT,
      path: path,
      src: `${urlEndpoint}${path}`
    };
  },
  methods: {
    onError(err) {
    console.log("Error");
    console.log(err);
  }, onSuccess(res) {
    console.log("Success");
    console.log(res);
  }},
};
</script>

<style>
.sample-app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>
