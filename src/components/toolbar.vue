<template>
    <div class="container">
        <ul class="toolbar">
            <li @click="onClick" v-for="tool in tools" :key="tool.id" class="toolbar-lists-item" :name="tool.name" :class="(tool.id==0)?'active':''">
                <toolbarItem :specs="tool"/>
            </li>
        </ul>
    </div>
</template>

<script>
    import toolbarItem from './toolbarItem.vue';
    import $ from 'jquery';
    export default{
        name: 'toolbar',
        components: {
            toolbarItem
        },
        data(){
            return{tools: [
                {id:0,name:'hand', icon: 'hand-pointer', shortkey:'0'},
                {id:1,name:'brush', icon: 'paint-brush', shortkey:'1'},
                {id:2,name:'magic pen', icon: 'magic', shortkey:'2'},
                {id:3,name:'pencil', icon: 'pencil-alt', shortkey:'3'},
                {id:4,name:'eraser', icon: 'eraser', shortkey:'4'},
            ]}
        },
        methods:{
            onClick(e){
                $('.active').removeClass('active')                
                $($(e.target).closest('li')).addClass('active')
                this.$emit('itemSelected',$($(e.target).closest('li')).attr('name'))
            }           
        },
        created() {            
            const component = this;
            this.handler = function (e) {
                if(e.which<48 || e.which>53)
                    return
                // this.$emit('keyup', e);
                console.log(e.which)
                let selectedToolId = e.which-48 //48 is ascii code for '0'
                $('.active').removeClass('active')
                $($('li.toolbar-lists-item')[selectedToolId]).addClass('active')
                component.$emit('itemSelected',$($('li.toolbar-lists-item')[selectedToolId]).attr('name'))
            }
            window.addEventListener('keyup', this.handler);
        },
        beforeUnmount() {
            window.removeEventListener('keyup', this.handler);
        }
    };
</script>
<style scoped>
    li{
        list-style-type: none;
        margin: 10px;
        padding: 10px;
        color: #aab;
        cursor: pointer;
        font-size: large;
        transition: all 0.2s ease-in-out;
    }
    li:first-child{
        border-bottom: 1px solid #aaa;
    }
    li:hover{
        transform: translateY(-2px);
        transform: scale(1.5)
    }
    li.active{
        color: #2a5;
        transform: scale(1.5)
    }
    ul{
        background-color: #334;
        text-align: left;
        padding: 10px;
        float:left;
    }
</style>