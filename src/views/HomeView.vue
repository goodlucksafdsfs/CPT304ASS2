<template>
  <div class="home">
   <div class="block">
  <span class="demonstration" style="margin-right:20px">选择地区</span>
  <el-select   placeholder="请选择所在国家"
    v-model="cont"
    :options="options"
    @change="handleContChange">
    <el-option
      v-for="item in contList"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
    </el-select>
  <!-- <el-cascader
  placeholder="请选择所在地区"
    v-model="value"
    :options="options"
    @change="handleChange"></el-cascader> -->
    <el-select   placeholder="请选择所在地区"
    v-model="value"
    :options="op1"
    @change="handleChange">
    <el-option
      v-for="item in op1"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
    </el-select>
    <el-select   placeholder="请选择节假日"
    v-model="holidayValue"
    @change="handleHoliDayChange">
    <el-option
      v-for="item in holiday"
      :key="item"
      :label="item"
      :value="item">
    </el-option>
    </el-select>
</div>
  <el-descriptions
    class="margin-top"
    title="地区信息"
    :column="2"
    :size="size"
    border
  >
    <el-descriptions-item>
      <template #label>
        <div class="cell-item">
          <el-icon :style="iconStyle">
            <user />
          </el-icon>
          天气
        </div>
      </template>
      {{obj.weather}}
    </el-descriptions-item>
    <el-descriptions-item>
      <template #label>
        <div class="cell-item">
          <el-icon :style="iconStyle">
            <iphone />
          </el-icon>
          公共假期
        </div>
      </template>
      <p v-for="item in obj.holiday" :key="item">{{item}}</p>
    </el-descriptions-item>

    <el-descriptions-item>
      <template #label>
        <div class="cell-item">
          <el-icon :style="iconStyle">
            <tickets />
          </el-icon>
          租赁信息
        </div>
      </template>
        <ul class="lease">
          <li v-for="(item,index) in obj.lease" :key="index">
            <img :src="item.img" alt="" />
         <div>
           <h3>{{item.title}}</h3>
           <p><span>价格：</span> {{item.price}}</p>
           <p><span>面积：</span> {{item.area}}</p>
         </div>
          </li>

          </ul>
    </el-descriptions-item>
  </el-descriptions>
  </div>
</template>

<script setup>
import { onMounted, reactive, ref } from 'vue'
      let contList=[{label:"中国",
      value:"中国"},{label:"美国",
      value:"美国"}]
  let options=[{
      label:"杭州",
      value:"杭州",
      weather:'晴 18­°C～28­°C',
      lease:[
       {
         img:'https://hwxypic.5i5j.com/images/hangzhou/20230210/a2f3e86b9f944db7a821694e83a4efb3.jpg',
         price:'300元/天',
         title:'滨江区政府·倾城之恋花园·4室',
         area:'80㎡'
       },
           {
         img:'https://hwxypic.5i5j.com/images/hangzhou/20230210/a2f3e86b9f944db7a821694e83a4efb3.jpg',
         price:'300元/天',
         title:'滨江区政府·倾城之恋花园·4室',
         area:'80㎡'
       },
           {
         img:'https://hwxypic.5i5j.com/images/hangzhou/20230210/a2f3e86b9f944db7a821694e83a4efb3.jpg',
         price:'300元/天',
         title:'滨江区政府·倾城之恋花园·4室',
         area:'80㎡'
       },
      ],
      holiday:[
        "劳动节：5月1日",
        "端午节:6月22日",
        "中秋节:9月29日",
        "端午节:9月30日",
      ]
    },
       {
      label:"上海",
      value:"上海",
      weather:'晴 18­°C～28­°C',
      lease:[
       {
         img:'https://aihome.aihome365.cn/2022/03/57119f56-0da1-42ee-9982-e47bc716a348.jpg?x-oss-process=style/P7',
         price:'200元/天',
         title:'整租·潮鸣·大学路新村·1室甄选',
         area:'80㎡'
       },
         
      ],
      holiday:[
        "劳动节：5月1日",
        "端午节:6月22日",
        "中秋节:9月29日",
        "端午节:9月30日",
      ]
    },
       {
      label:"广州",
      value:"广州",
      weather:'晴 28­°C～38­°C',
      lease:[
       {
         img:'https://aihome.aihome365.cn/2022/08/4b71e1b5-de3f-4c47-8aa8-26a1d7f29032.jpg?x-oss-process=style/P7',
         price:'100元/天',
         title:'整租·鼓楼·勤远里·2室甄选',
         area:'80㎡'
       },
      
      ],
      holiday:[
        "劳动节：5月1日",
        "端午节:6月22日",
        "中秋节:9月29日",
        "端午节:9月30日",
      ]
    },
        {
      label:"苏州",
      value:"苏州",
      weather:'晴 28­°C～38­°C',
      lease:[
       {
         img:'https://aihome.aihome365.cn/2022/08/4b71e1b5-de3f-4c47-8aa8-26a1d7f29032.jpg?x-oss-process=style/P7',
         price:'90元/天',
         title:'整租·鼓楼·勤远里·2室甄选',
         area:'80㎡'
       },
      
      ],
      holiday:[
        "劳动节：5月1日",
        "端午节:6月22日",
        "中秋节:9月29日",
        "端午节:9月30日",
      ]
    }
      
   
  ]
  let options2=[{
      label:"洛杉矶",
      value:"洛杉矶",
      weather:'晴 18­°C～28­°C',
      lease:[
       {
         img:'https://hwxypic.5i5j.com/images/hangzhou/20230210/a2f3e86b9f944db7a821694e83a4efb3.jpg',
         price:'1005美元/天',
         title:'The Lorenzo',
         area:'80㎡'
       },
           {
         img:'https://hwxypic.5i5j.com/images/hangzhou/20230210/a2f3e86b9f944db7a821694e83a4efb3.jpg',
         price:'825美元/天',
         title:'Victory on Portpand',
         area:'80㎡'
       },
           {
         img:'https://hwxypic.5i5j.com/images/hangzhou/20230210/a2f3e86b9f944db7a821694e83a4efb3.jpg',
         price:'2450美元/天',
         title:'West 27th Place',
         area:'80㎡'
       },
      ],
      holiday:[
        "新年 1月1日",
"情人节 2月14日",
"圣诞节 12月25日",
"复活节 4月20日",
"万圣节 11月1日"
      ]
    },
       {
      label:"芝加哥",
      value:"芝加哥",
      weather:'晴 18­°C～28­°C',
      lease:[
       {
         img:'https://aihome.aihome365.cn/2022/03/57119f56-0da1-42ee-9982-e47bc716a348.jpg?x-oss-process=style/P7',
         price:'1089美元/天',
         title:'Tailor Lofts',
         area:'80㎡'
       },
       {
         img:'https://aihome.aihome365.cn/2022/03/57119f56-0da1-42ee-9982-e47bc716a348.jpg?x-oss-process=style/P7',
         price:'975美元/天',
         title:'The Latterman Chicago',
         area:'80㎡'
       },
      ],
      holiday:[
        "新年 1月1日",
"情人节 2月14日",
"圣诞节 12月25日",
"复活节 4月20日",
"万圣节 11月1日"
      ]
    },
       {
      label:"纽约",
      value:"纽约",
      weather:'晴 28­°C～38­°C',
      lease:[
       {
         img:'https://aihome.aihome365.cn/2022/08/4b71e1b5-de3f-4c47-8aa8-26a1d7f29032.jpg?x-oss-process=style/P7',
         price:'4079美元/天',
         title:'Lyra',
         area:'80㎡'
       },
      
      ],
      holiday:[
        "新年 1月1日",
"情人节 2月14日",
"圣诞节 12月25日",
"复活节 4月20日",
"万圣节 11月1日"
      ]
    },
        {
      label:"华盛顿",
      value:"华盛顿",
      weather:'晴 28­°C～38­°C',
      lease:[
       {
         img:'https://aihome.aihome365.cn/2022/08/4b71e1b5-de3f-4c47-8aa8-26a1d7f29032.jpg?x-oss-process=style/P7',
         price:'1950美元/天',
         title:'Andover House',
         area:'80㎡'
       },
      
      ],
      holiday:[
        "新年 1月1日",
"情人节 2月14日",
"圣诞节 12月25日",
"复活节 4月20日",
"万圣节 11月1日"
      ]
    }
      
   
  ]
  let value=ref('')//默认选择地区
  let cont=ref('')//默认选择地区
  let holidayValue=ref('')
  let obj=reactive({//查询结果
    
  })
  let op1=ref([])
let  holiday=ref([])
let l=[
        "劳动节：5月1日",
        "端午节:6月22日",
        "中秋节:9月29日",
        "端午节:9月30日",
      ]

      let s=[
        "新年 1月1日",
"情人节 2月14日",
"圣诞节 12月25日",
"复活节 4月20日",
"万圣节 11月1日"
      ]
  const handleHoliDayChange=(e)=>{//监听选择事件触发
    console.log(e,'handleChange');
    let data=op1.value.filter(res=>{//通过过滤查询到符合选择城市的信息
       return res.value==value.value&&res.holiday.includes(e)
     })[0]
     console.log(data,'data');
     for(let key in data){//将查询到的信息储存到obj对象中
       obj[key]=data[key]
     }
  }
  
  const handleContChange=(e)=>{//监听选择事件触发
    console.log(e,'handleChange');
    if(e=='中国'){
      op1.value=options
      holiday.value=l
      console.log(holiday,'holiday');
    }else if(e=='美国'){
      op1.value=options2
      holiday.value=s
      console.log(holiday,'holiday');
    }else{
      op1.value=[]
      holiday.value=[]

    }
  }
  const handleChange=(e)=>{//监听选择事件触发
    console.log(e,'handleChange');
  //  let data=options.filter(res=>{//通过过滤查询到符合选择城市的信息
  //      return res.value==e
  //    })[0]
  //    console.log(data,'data');
  //    for(let key in data){//将查询到的信息储存到obj对象中
  //      obj[key]=data[key]
  //    }
  }
  onMounted(()=>{//生命周期 
    handleChange([value.value])//初始化调用查询方法 设置默认值（苏州）
  })
</script>
<style>
 .home{
   height: 100vh;
   width: 100vw;
   padding: 30px;
   box-sizing: border-box;
 }
.lease img{
  width: 100px;
  height: 100px;
  margin-right: 20px;
}
.lease>li{
  list-style-type: none;
 display: flex;
 align-content: flex-start;
 margin-bottom: 20px;
 border-bottom: 1px solid #f3f3f3;
 padding: 20px;
}
</style>