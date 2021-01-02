<template>
    <div class="input-number">
        <input type="text" :value="curentValue" @change="handelChange">
        <button :disabled="curentValue<= min" @click="handleDown">-</button>
        <button :disabled="curentValue>= max"  @click="handleUp">+</button>
    </div>
</template>

<script>
    function isValueNumber (value) {
        console.log('isValueNumber: ', isValueNumber);
        return (/(^-?[0-9]+\.{1}\d+$) | (^-?[1-9][0-9] *$) | (^-?[1-9][0-9]*$) | (^-?0{1}$) /).test(value + '')
    }
    export default {
        name:'input-number',
        data(){
            return {
                curentValue:this.value
            }
        },
        watch:{
            curentValue:function(val){
                this.$emit('input',val)
                this.$emit('on-change',val)
            },
            value(val){
                console.log('updateValue runed');
                this.updateValue(val)
            }
        },
        methods:{
            updateValue(val){
                if (val > this.max) {val = this.max}
                if (val < this.min) {val = this.min}
                this.curentValue = val
            },
            handelChange(e){
                console.log('e: ', e);
                var val = e.target.value.trim()
                var max = this.max
                var min = this.min

                if(isValueNumber(val)){
                    console.log('isValueNumber(val): ', isValueNumber(val));
                    val = Number(val)
                    this.curentValue = val

                    if(val > max){
                        this.curentValue = max
                    }else if(val < min) {
                        this.curentValue = min
                    }
                } else {
                    event.target.value = this.curentValue
                }

            },
            handleDown(){
                this.curentValue --
                },
            handleUp(){
                this.curentValue ++ 
            }
        },
        props:{
            max:{
                type:Number,
                default:Infinity,
            },
            min:{
                type:Number,
                default:-Infinity,
            },
            value:{
                type:Number,
                default:0,
            },
        },
        mounted(){
            this.updateValue(this.value)
        }
    
    }
</script>

<style scoped>
    .input-number {
        background:lightblue;
    }
</style>