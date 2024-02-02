 <template>
    <div>
      <h2>{{ radioName }}</h2>
      <audio :src="streamUrl" controls autoplay></audio>
    </div>
  </template>
  
  <script>
  export default {
    props: ['streamUrl', 'radioName', 'imageUrl'],
  };
  
  </script>
  