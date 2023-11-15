<script setup>
// import Navbar from '../components/Navbar.vue'
import Card from '../components/Card.vue'
// import Footer from '../components/Navbar.vue'
import { ref } from 'vue'
import Clipboard from 'clipboard'
import isUrlHttp from 'is-url-http'


const originalLink = ref('')
const links = ref([])


function shortenLink() {
  const url = `https://csclub.uwaterloo.ca/~phthakka/1pt-express/addURL?long=${originalLink.value}`
  // check if the url is valid
  if (isUrlHttp(originalLink.value)) {
    fetch(url, {
      method: 'POST',
      headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json',
      },
      // body: JSON.stringify(data)
    })
    .then(res => {
      return res.json()
    })
    .then(data => {
      console.log(data)
      links.value.push({
        'long': data.long,
        'short': `https://1pt.co/${data.short}`
      })

      // reset form
      originalLink.value = ''
  })
    .catch(err => {
      console.error(err);
    })
  }
  else {
    console.log("invalid url or no url provided")
  }


}

function copyToClipboard(shortLink) {
  const clipboard = new Clipboard('.copy-btn', {
    text: function () {
      return shortLink;
    }
  });

  clipboard.on('success', function (e) {
    console.log('Copied to clipboard');
    e.clearSelection();
  });

  clipboard.on('error', function (e) {
    console.error('Unable to copy to clipboard');
  });

  clipboard.destroy();
}

function removeCard(link) {
  links.value = links.value.filter((l) => l !== link)
}

</script>

<template>
    <input type="text" v-model="originalLink">
    <button @click="shortenLink">Shorten</button>
    <div v-for="(link, index) in links" :key="index">
      <Card :long="link.long" :short="link.short" @copy="copyToClipboard(link.short)" @remove="removeCard(link)"/>
      <!-- <div>
        {{ link.long }} {{ link.short }} 
        <button @click="copyToClipboard(link.short)">Copy to clipboard</button>
        <button @click="removeCard(link)">Delete</button>
      </div> -->
    </div>
</template>
