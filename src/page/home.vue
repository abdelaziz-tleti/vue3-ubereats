<template>
  <div class="home">
    <RestautantRow/>
  </div>
</template>

<script>
import BDD from '../BDD';
import RestautantRow from '@/components/RestautantRow.vue';

export default {
name: 'HomePage',
components:{
RestautantRow,
},
setup(){
    class Restautant{
        constructor(name, note, image,drive_time){
            this.name = name;
            this.note = note;
            this.image = image;
            this.drive_time = drive_time;
        }
    }
    var resto = new Restautant('resto', 4.5, 'img', '45');
    console.log(BDD);
    console.log(resto);
}
}
</script>

<style>

</style>