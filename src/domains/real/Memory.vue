<template>
  <div class="i-part" v-bind:style="style">
  </div>
</template>

<script>
import Vue from "vue"

import MixinDomain from "../../core/mixin/Domain.js"
import MixinEntity from "../../core/mixin/Entity.js"

import VisualMemory from '../visual/Memory.vue'
import RealMemoryView from './MemoryView.vue'
import RealMemoryView1 from './MemoryView1.vue'


export default {
    mixins: [ MixinDomain, MixinEntity ],

    name: 'RealMemory',

    props: {
        position: Array,
    },

    data() {
        return {
            title: "内存",
        }
    },

    computed: {
        style () {
            return {
                left: this.position[ 0 ] + 'px',
                top: this.position[ 1 ] + 'px',
                width: '30px',
                height: '30px',
            }
        }
    },

    mounted() {
        let visualMemory = Vue.extend( VisualMemory )
        let memory = new visualMemory()
        memory.$mount()
        this.mapStack.push( memory )

        let RealMemoryViewObject = Vue.extend( RealMemoryView )
        let view = new RealMemoryViewObject( {
            propsData: {
                basestone: this
            }
        } )
        view.$mount()
        this.viewStack.push( view )

        RealMemoryViewObject = Vue.extend( RealMemoryView1 )
        view = new RealMemoryViewObject( {
            propsData: {
                basestone: this
            }
        } )
        view.$mount()
        this.viewStack.push( view )
    },

    methods: {

        doActionRead ( addr, size ) {
        },

        doActionWrite ( addr, size, value ) {
        },

    },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.i-part {
    background-image: url("../../assets/sim.svg");
    background-size: cover;
}
</style>
