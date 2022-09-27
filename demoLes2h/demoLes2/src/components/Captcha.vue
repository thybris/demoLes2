<script setup lang="ts">
import { onMounted, ref } from 'vue'

const emit = defineEmits(['correct', 'incorrect']);
const props = defineProps({
    seconds: {
        type: Number,
        required: false,
        default: 0,
    }
})

const secondsLeft = ref()

const captchaElements = ref([
    {
        image: 'https://image.shutterstock.com/image-photo/skeptic-surprised-cat-thinking-dont-260nw-1905929728.jpg',
        isSelected: false,
        isfunny: true,
    },
    {
        image:'https://www.rd.com/wp-content/uploads/2019/09/GettyImages-621924830-scaled.jpg',
        isSelected: false,
        isfunny: true,
    },
    {
        image:'https://media.s-bol.com/grOq0M7nypG/550x827.jpg',
        isSelected: false,
        isfunny: true,
    },
    {
        image:'https://cdn.pixabay.com/photo/2015/04/23/22/00/tree-736885__480.jpg',
        isSelected:false,
        isfunny: false,
    }
]);

const confirm = function() {
    console.log("User clicked the confirm button");

    const isCorrect = captchaElements.value.reduce(
        (result, captchaObj) =>  result && (captchaObj.isfunny == captchaObj.isSelected), true
    )

     console.log(`IsCorrect? ${isCorrect}`);

     emit(isCorrect? 'correct' : 'incorrect');

    
};

onMounted(() => {
        console.log("On Mounted ...")

        setInterval(() => {

        }, 1000);
     })



</script>

<template>
    <div>
        <img class="image" 
                v-for="(item, i) in captchaElements" 
                            :src="item.image" 
                            :key="`cpt${i}`"
                            :class="{selected: item.isSelected}"
                            @click="item.isSelected =! item.isSelected"
        />

        <button @click="confirm">Verify Captcha</button>
    </div>
    
    
</template>

<style scoped>
    .image {
        width: 100px;
        height: 100px;
        margin: 10px;
        border: solid grey 4px;
        object-fit: contain;
    }

    .selected {
        border: solid lime 4px;
    }

</style>