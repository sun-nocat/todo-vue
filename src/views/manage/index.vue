<template>
    <div class="manage tc">
        <button @click="add">新增</button>
        <div class="input-area" v-show="showAdd">
            <input type="text" placeholder="请输入姓名" v-model="nameValue" @enter='addName'>
            <button @click="addName">确定</button>
        </div>
        <table>
            <tr>
                <th>姓名</th>
                <th>操作</th>
            </tr>
            <tr v-for = "(name,index) in people">
                <td>
                    {{name.name}}
                </td>
                <td :id="index">
                    <span @click="edit(index,name)">
                        编辑
                    </span>
                    <span @click="del(index)">
                        删除
                    </span>
                </td>
            </tr>
        </table>

        <div class="wrap" v-show="showEdit">
            <div class="content">

                <input type="text" placeholder="请输入新姓名" v-model="newName">
                <button @click="cancel">取消</button>
                <button @click="editName">确认</button>
            </div>
        </div>

        <footer-nav></footer-nav>
    </div>

</template>


<script>
import footerNav from "../../components/footer";
export default {
  components: {
    footerNav
  },
  data: function() {
    return {
      showAdd: false,
      newName: "",
      nameValue: "",
      showEdit: false,
      editId: "",
      people: [{ name: "sun" }, { name: "ming" }]
    };
  },
  methods: {
    add: function() {
      this.showAdd = true;
    },
    addName: function() {
      if (this.nameValue != "") {
        var data = {
          name: this.nameValue
        };
        console.log(data);

        this.people.push(data);
        this.nameValue = "";
      } else {
        alert("不能使用空");
      }
    },

    del: function(index) {
      this.people.splice(index, 1); //js根据数组的索引刪除列表中的元素
    },
    edit: function(index, name) {
      this.newName = name.name;
      this.editId = index;
      this.showEdit = true;
    },
    cancel: function() {
      console.log(this);
      this.showEdit = false;
    },
    editName: function() {
      if (this.newName != "") {
        console.log(this.editId);
        console.log(this.newName);
        this.people[this.editId].name = this.newName;
        this.showEdit = false;
      }
    }
  }
};
</script>


<style>
.manage {
  padding-bottom: 50px;
}
.manage > button {
  width: 200px;
  height: 40px;
  line-height: 40px;
  background-color: #41b883;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  color: #fff;
}
table {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  margin-top: 20px;
}
.input-area input {
  width: 200px;
  height: 40px;
  line-height: 40px;
  margin: 20px 0;
  outline: none;
  border: 1px solid #333;
}
.input-area button {
  width: 60px;
  height: 40px;
  line-height: 40px;
  background-color: #41b883;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  color: #fff;
}
th,
td {
  width: 100px;
}
tr input {
  width: 100px;
  height: 30px;
  padding-left: 10px;
  outline: none;
  border: 1px solid #333;
}
.wrap {
  display: table;
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background: rgba(0, 0, 0, 0.8);
  z-index: 10;
}
.wrap .content {
  display: table-cell;
  vertical-align: middle;
}
.wrap .content input {
  height: 40px;
  line-height: 40px;
  display: block;
  margin: 0 auto;
  margin-bottom: 10px;
  font-size: 16px;
}
.wrap .content button {
  width: 100px;
  height: 30px;
  line-height: 30px;
  background-color: #41b883;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  color: #fff;
}
</style>