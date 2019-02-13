<template>
    <div class="todolist">
        <div class="header">
            <span class="txt">Todolist</span>
            <input type="text" v-model="msg" placeholder="添加Todo..." class="content"   @keyup.enter="add">
           
        </div>
        <div class="unfinished">
            <p>未完成 
                <input type="text" class="num" v-model="num" readonly>
            </p>
            <ul  >
                <li v-for="(item,index) in todolist" :data-index="index" :key="item.id" :aria-id="item.id" ref="li" @click="selectcheck">
                    <span class="bar"></span>
                    <el-checkbox   class="checkbox" >{{item.content}}</el-checkbox>
                    <input type="button" value="-" class="del" >
                </li>
                
            </ul>
        </div>
        <div class="complate">
            <p>已完成
                 
            </p>
            <ul>
                 <li v-for="(item,index) in comlist" :data-index="index"  :key="item.id" @click="selectcomlist">
                    <span class="bar"></span>
                    <el-checkbox  class="checkbox">{{item.content}}</el-checkbox>
                    <input type="button" value="-" class="del">
                </li>
                
            </ul>
        </div>
        <div class="clear">
            <p>todolist@2019 <span class="clear-gray" @click="clearAll">clear</span></p>
        </div>
    </div>
</template>
<script>
export default {
  data(){
      return {
          checked: false,
          msg:'',
          id:0,
          num:0,
          todolist:[
              

          ],
          comlist:[
              
          ] //已经完成的数组


      }
  } ,
  created(){
      
  },
  methods:{
      selectcheck:function(e){
          //选框点击事件
          let dom = e.target
          
          let currentdom= e.currentTarget
          let index = currentdom.getAttribute("data-index")
        //   console.log(currentdom)
        //   console.log(dom)
           if(dom.value=="-"){
            //    console.log("shan"+index)
                this.todolist.splice(index,1);
                
            }
            
          
        
         if(dom.type=="checkbox"){
             
             let comment = this.todolist.splice(index,1);
            //  console.log(comment[0])
             this.comlist.unshift(comment[0])
         }
         this.num=this.todolist.length
      },
     selectcomlist:function(e){
           //选框点击事件
          let dom = e.target
          let currentdom= e.currentTarget
          let index = currentdom.getAttribute("data-index")
          console.log(dom)
           if(dom.value=="-"){
                this.comlist.splice(index,1);
            }
            
          
        
         if(dom.type=="checkbox"){
             
             let comment = this.comlist.splice(index,1);
             console.log(comment[0])
             this.todolist.push(comment[0])
         }
     },
      add(){
          //监听键盘enter事件
          this.content=this.msg
          this.id=this.todolist.length
          this.msg=""
          this.id++
          var lio = {id:this.id,content:this.content}
          this.todolist.push(lio)
          this.num=this.todolist.length
         
          
     },
     clearAll(){
         this.todolist=[]
         this.comlist=[]
     },
    
    
  } 
}
</script>

<style lang="scss">
.todolist{
    background-color: #eee;
    width: 100%;
    height:650px;
    .header{
       width: 100%;
       height: 40px;
       background-color: #026;
       position:relative;
       .txt{
           color:#fff;
           font-style:italic;
           position: absolute;
           top: 10px;
           left: 10px;
           
       }
       .content{
           outline: none;
           width: 50%;
           height: 20px;
           margin: 10px 0;
           border:none;
           padding-left: 5px;
           border-radius: 5px;
           
       }
       
    }
    .unfinished{
        p{
            color:#000;
            font-weight:700;
            position: relative;
            .num{
                position: absolute;
                top: 0;
                right: 30px;
                z-index: 99;
                width: 18px;
                height: 18px;
                outline: none;
                border:none;

                color:#555;
                border-radius: 50%;
                font-size: 12px;
                line-height: 18px;
                text-align: center;
                background-color: rgba(111, 171, 206, 0.268);
            }
        }
        ul{
           
            li{
               
                position: relative;
                list-style: none;
                width: 300px;
                 height: 20px;
                 background-color: #fff;
                 margin-bottom: 8px;
                 border-radius: 3px;
                .bar{
                    position:absolute;
                    top: 0;
                    left: 0;
                    width: 3px;
                    height:20px;
                    background-color: rgb(0, 132, 255);
                    z-index: 999;
                    border-radius: 2px;
                    
                }
                .checkbox{
                    position:absolute;
                    top: 0;
                    left: 10px;
                    color:#333;
                }
                .del{
                    position: absolute;
                    top: 2px;
                    right: 15px;
                    outline: none;
                    border-radius: 50%;
                    border:none;
                    width: 16px;
                    height:16px;
                    color:#f00;
                }
            }
        }
    }
    .complate{
         p{
            color:#000;
            font-weight:700;
           
        }
          ul{
            li{
                
                position: relative;
                list-style: none;
                width: 300px;
                height: 20px;
                background-color: #fff;
                margin-bottom: 5px;
                .bar{
                    position:absolute;
                    top: 0;
                    left: 0;
                    width: 3px;
                    height:20px;
                    background-color: #ccc;
                    z-index: 999;
                    border-radius: 2px;
                }
                .checkbox{
                    position:absolute;
                    top: 0;
                    left: 10px;
                    color:#ccc;
                }
                .del{
                    position: absolute;
                    top: 2px;
                    right: 15px;
                    outline: none;
                    border-radius: 50%;
                    border:none;
                    width: 16px;
                    height:16px;
                    color:#999;
                }
            }
        }
    }
    .clear{
        p{
            color:#333
        }
        .clear-gray{
            color:gray;
        }
    }
}
</style>
