<template>
  <div class="app-container">
    <el-card shadow="never">
      <div slot="header" class="clearfix">
        <span>基本信息</span>
      </div>
      <div>
        <el-form ref="form" :model="form" label-width="120px" :rules="rules">
          <el-row>
            <el-col :span="12">
              <el-form-item label="商品名称:" prop="name">
                <el-input v-model="form.name"></el-input>
              </el-form-item></el-col>
            <el-col :span="12">
              <el-form-item label="权重:" prop="name">
                <el-input v-model="form.name"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="24">
              <el-form-item label="搜索关键词:" prop="name">
                <el-input v-model="form.name" placeholder='多个关键词请用"|"分隔开'></el-input>
              </el-form-item></el-col>

          </el-row>
          <el-row>
          <el-col :span="6">
              <el-form-item label="商品标签分类:" prop="region">
                <el-select v-model="form.region" width="100%" placeholder="商品标签分类">
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item>
            </el-col>
         

            <el-col :span="6">
              <el-form-item label="商品分类:" prop="region">
                <el-select v-model="form.region" width="100%" placeholder="商品分类">
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>

            <el-col :span="6">
              <el-form-item label="销售价格:">

                <el-input placeholder="" v-model="form.num">
                  <template slot="append">元</template>
                </el-input>
              </el-form-item>

            </el-col>
            <el-col :span="6">
              <el-form-item label="库存:">
                <el-input-number :min="0" v-model="form.num" :step="1"></el-input-number>
              </el-form-item>

            </el-col>
            <el-col :span="6">
              <el-form-item label="已出售数:">
                <el-input-number :min="0" v-model="form.num" :step="1"></el-input-number>
              </el-form-item>

            </el-col>
            <el-col :span="6">
              <el-form-item label="是否显示销量">
                <el-switch active-text="是" inactive-text="否" v-model="form.delivery"></el-switch>
              </el-form-item>

            </el-col>


          </el-row>
          <el-row>
            <el-col :span="24">
              <el-form-item label="商品图片:">
                <ImageUpload v-model="form.img"></ImageUpload>
              </el-form-item>

            </el-col>
            <el-col :span="24">
              <el-form-item label="商品图详情:">
                <ImageUpload v-model="form.img"></ImageUpload>
              </el-form-item>

            </el-col>
          </el-row>


          <el-row>
            <el-col>
              <el-form-item label="规格:">
                <el-button @click="handleAddSpecifications" type="primary">新增规格</el-button>
              </el-form-item>

            </el-col>
          </el-row>
          <el-row>


            <el-col :span="6">
              <el-form-item label="是否上架:">
                <el-switch active-text="是" inactive-text="否" v-model="form.delivery"></el-switch>
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="是否包邮:">
                <el-switch active-text="是" inactive-text="否" v-model="form.delivery"></el-switch>
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="邮费:">
                <el-input-number :min="0" v-model="form.num" :step="1"></el-input-number>
              </el-form-item>
            </el-col>

          </el-row>
          <el-row>
            <el-col :span="6">
              <el-form-item label="购买三倍积分:">
                <el-switch active-text="是" inactive-text="否" v-model="form.delivery"></el-switch>
              </el-form-item>
            </el-col>

            <el-col :span="6">
              <el-form-item label="购买送抽奖券:">
                <el-switch active-text="是" inactive-text="否" v-model="form.delivery"></el-switch>
              </el-form-item>
            </el-col>
            <el-col :span="6">
              <el-form-item label="是否推荐商品:">
                <el-switch active-text="是" inactive-text="否" v-model="form.delivery"></el-switch>
              </el-form-item>
            </el-col>

          </el-row>
          <el-row>

            <el-col :span="24">
              <el-form-item>
                <el-button type="primary" @click="onSubmit">保存</el-button>
              </el-form-item>
            </el-col>

          </el-row>
        </el-form>
      </div>
    </el-card>

    <!-- 添加规格 -->
    <el-dialog title="新增规格" :visible.sync="centerDialogVisible" width="50%" center :close-on-click-modal="false">
      <el-form ref="form" :model="form" label-width="100px">
        <el-row>
          <el-col :span="24">
            <el-form-item label="规格名称:">
              <el-input v-model="form.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item label="规格参数:">
              <div class="item-input-icon">
                <el-input v-model="form.name"></el-input>
                <i class="el-icon-remove-outline imgFont"></i>
              </div>
            </el-form-item>
          </el-col>
          <el-col :span="24">
            <el-form-item>
              <el-button type="primary" icon="el-icon-plus">新增规格参数(必须)</el-button>
            </el-form-item>

          </el-col>

        </el-row>
      </el-form>

      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script>
import ImageUpload from '@/components/Upload/ImageUpload'

export default {
  components: { ImageUpload },

  data() {
    return {
      form: {
        img:'https://occ.hnous.net/group1/M00/00/00/rByNf2MIbFGADkFAAAFqcAxKMRI548.png',
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: '',
        num: 1
      },
      rules: {
        name: [
          { required: true, message: '请输入商品名称', trigger: 'blur' }
        ],
        region: [
          { required: true, message: '请输入商品标签分类', trigger: 'blur' }
        ],
      },
      centerDialogVisible: false
    }


  },
  computed: {},
  methods: {
    onSubmit() {
      console.log('submit!');
    },

    handleAddSpecifications() {
      this.centerDialogVisible = true
    }
  }
}
</script>
<style scoped>
.el-select:v-deep{
  width: 100%;
}

.imgFont {
  font-size: 30px;
  cursor: pointer;
  margin-left: 10px;
}

.item-input-icon {
  display: flex;
  flex-direction: row;
  align-items: center;
}
</style>