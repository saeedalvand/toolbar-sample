<template>
    <span class="toolbar-item">
        <i :class="faIcon" :title="this.title"></i>
        {{specs.length}}
    </span>
</template>

<script>
    export default{
        name: 'toolbarItem',
        props: ['specs'],
        computed: {
            faIcon(){
                return 'fas fa-'+this.specs.icon;
            },
            title(){
                return this.specs.name + ', shortkey: ' + this.specs.shortkey;
            }
        }
    };
</script> 
