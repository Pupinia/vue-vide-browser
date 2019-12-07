<template>
  <div>
    <SearchBar @termChange="onTermChange"></SearchBar>
    <VideoList />
    {{ videos.length }}
  </div>
</template>

<script>
import axios from "axios";

import SearchBar from "@/components/SearchBar";
import VideoList from "@/components/VideoList";
const API_KEY = "AIzaSyCv0EbN-75eUlg_xDVHGgloK2cuN7oEglk";

export default {
  name: "App",
  components: {
    SearchBar,
    VideoList
  },
  data() {
    return { videos: [] };
  },
  methods: {
    onTermChange(serchTerm) {
      axios
        .get("https://www.googleapis.com/youtube/v3/search", {
          params: {
            key: API_KEY,
            type: "video",
            part: "snippet",
            q: serchTerm
          }
        })
        .then(response => (this.videos = response.data.items));
    }
  }
};
</script>