<template>
    <div :class="wrapClasses" :style="styles">
        <div :class="classes">  
            <div :class="[prefixCls + '-title']" v-if="showSlotHeader" ref="title">
                <slot name="header"></slot>
            </div>
            <div :class="[prefixCls + '-header']" v-if="showHeader" ref="header" @mousewheel="handleMouseWheel">
                <table-head
                    :prefix-cls="prefixCls"
                    :styleObject="tableStyle"
                    :columns="cloneColumns"
                    :obj-data="objData"
                    :columns-width="columnsWidth"
                    :data="rebuildData"></table-head>
            </div>
            <div :class="[prefixCls + '-body']" :style="bodyStyle" ref="body" @scroll="handleBodyScroll"
                v-show="!((!!localeNoDataText && (!data || data.length === 0)) || (!!localeNoFilteredDataText && (!rebuildData || rebuildData.length === 0)))">
                <!-- <table-body
                    ref="tbody"
                    :prefix-cls="prefixCls"
                    :styleObject="tableStyle"
                    :columns="cloneColumns"
                    :data="rebuildData"
                    :columns-width="columnsWidth"
                    :obj-data="objData"></table-body> -->
            </div>
        </div>
    </div>
</template>
<script>
    import tableHead from './data-grid-head.vue';
    import tableBody from './data-grid-body.vue';

    import { oneOf, getStyle, deepCopy, getScrollBarSize } from '../../utils/assist';
    import { on, off } from '../../utils/dom';

    const prefixCls = 'ivu-table';

    let rowKey = 1;
    let columnKey = 1;

    export default {
        name: 'DataGrid',
        mixins: [ Locale ],
        components: { tableHead, tableBody },
        props: {
            columns:{
                type: Array,
                default:[]
            },
            dataSource:{
                type: Object,
                default:{}
            },
        },
        data () {
            return {
                ready: false,
                tableWidth: 0,
                columnsWidth: {},
                prefixCls: prefixCls,
                compiledUids: [],
                objData: this.makeObjData(),     // checkbox or highlight-row
                rebuildData: [],    // for sort or filter
                cloneColumns: this.makeColumns(),
                showSlotHeader: true,
                showSlotFooter: true,
                bodyHeight: 0,
                bodyRealHeight: 0,
                scrollBarWidth: getScrollBarSize(),
                currentContext: this.context,
                cloneData: deepCopy(this.data)
            };
        },
        computed: {
            
        },
        methods: {
            
        }
    };
</script>
