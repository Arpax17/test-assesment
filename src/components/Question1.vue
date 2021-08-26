<template>
    <b-card>
        <b-form>
            <h6>Question 1</h6>
            <br>
            <b-row>
                <b-form-group class="col-md-5">
                    <label>Original Message: </label>
                    <b-form-input v-model="message" />
                </b-form-group>
                <b-form-group class="col-md-12">
                    <p>Message in Lowercase : {{message.toLowerCase().trim()}}</p>
                </b-form-group>    
            </b-row>
        </b-form>
    </b-card>
<!-- <div class="container-fluid">
      <p>Original message: </p><input v-model="message" >

       <p>Message in Lowercase: {{ message }}</p>
      
</div> -->

</template>

<script>
export default {
  data() {
    return {
        message:''
    }
  },

  created() {
  },

  methods: {
  }
}
</script>