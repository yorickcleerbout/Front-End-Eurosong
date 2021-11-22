<template>
    <div>
        <div :class="'c-feedback ' + classType" v-if="isActive" @click="hide">{{ message }} </div>

    </div>
</template>

<script>
export default {
    name: 'Feedback',
    props: [
        'message',
        'classType'
        ],
    data(){
        return {
            isActive: true
        }
    },
    methods: {
        hide() {
            this.isActive = false
        }
    }
        
    
}
</script>