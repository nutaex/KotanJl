<template>
  <div class="AddBuyerPop">
    <el-dialog center title="Purchaser Details" :visible.sync="show" width="40%" append-to-body @closed="closedForm">
      <div class="AddBuyerPop_box">
        <el-form ref="form_buyser" :rules="rules" :model="buyerForm" label-width="150px" v-if="show">
          <el-form-item label="Name" prop="buyerName">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.buyerName" :disabled="!!porjectInfo.isOpening && developers !== 2"></el-input>
          </el-form-item>
          <el-form-item label="Customer Type" prop="customerType">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.customerType">
              <el-option v-for="(item, index) in SellBlockData.CustomerTypeData" :key="index" :label="item.name" :value="item.value"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Date of Birth" prop="dateOfBirth">
            <!-- <el-date-picker
              value-format="yyyy-MM-dd"
              size="mini"
              type="date"
              v-model="buyerForm.dateOfBirth"
              style="width: 100%"
            ></el-date-picker> -->
            <datepicker class="buyerFormDatePicker" :disabled-dates="disabledDates" inputClass="DatePickerInputClass" v-model="buyerForm.dateOfBirth" :minimumView="'day'" :maximumView="'year'" :initialView="'year'">
            </datepicker>
          </el-form-item>
          <el-form-item label="Gender" prop="gender">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.gender">
              <el-option v-for="(item, index) in SellBlockData.GenderData" :key="index" :label="item.name" :value="item.value"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Area Code" prop="countryCallingCode">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.countryCallingCode">
              <el-option v-for="(item, index) in SellBlockData.countryCallingCodeData" :key="index" :label="item.name" :value="item.name"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Mobile" prop="buyerMobile">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.buyerMobile"></el-input>
          </el-form-item>
          <el-form-item label="Email" prop="buyerEmail">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.buyerEmail"></el-input>
          </el-form-item>
          <el-form-item label="Nationality" prop="nationality">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.nationality" :disabled="!!porjectInfo.isOpening && developers !== 2">
              <el-option v-for="(item, index) in SellBlockData.CitizenshipData" :key="index" :label="item" :value="item"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="NRIC/Passport" prop="nricPassport">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.nricPassport" :disabled="!!porjectInfo.isOpening && developers !== 2"></el-input>
          </el-form-item>
          <el-form-item label="Occupation">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.occupation"></el-input>
          </el-form-item>
          <el-form-item label="Residential">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.residential">
              <el-option v-for="(item, index) in SellBlockData.residentialData" :key="index" :label="item" :value="item"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="District">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.district">
              <el-option v-for="(item, index) in SellBlockData.DistrictData" :key="index" :label="item" :value="item">
              </el-option>
            </el-select>
          </el-form-item>

          <h4 style="margin-bottom: 15px; text-align: center">
            Current Residential Address
          </h4>

          <el-form-item label="Country">
            <el-select size="mini" style="width: 100%" v-model="buyerForm.country">
              <el-option v-for="(item, index) in SellBlockData.CitizenshipData" :key="index" :label="item" :value="item"></el-option>
            </el-select>
          </el-form-item>
          <el-form-item label="Block">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.block"></el-input>
          </el-form-item>
          <el-form-item label="# Unit">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.unitNo"></el-input>
          </el-form-item>
          <el-form-item label="Postal Code">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.postalCode"></el-input>
          </el-form-item>
          <el-form-item label="Street Name">
            <el-input size="mini" style="width: 100%" v-model="buyerForm.streetName"></el-input>
          </el-form-item>
        </el-form>
      </div>
      <div slot="footer" class="dialog-footer">
        <el-button @click="show = false">Cancel</el-button>
        <el-button type="primary" @click="addDataFn">Save</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import SellBlockData from '../../SalesBooking/SalesFlowchart/commponents/SellBlockData.json'
import { setRulesData } from '@/utils/validate'
import Datepicker from 'vuejs-datepicker'
export default {
  components: { Datepicker },
  props: {
    buyFom: {
      type: Object,
      default: () => { },
    },
  },
  inject: ['porjectInfo'],
  data () {
    return {
      show: false,
      buyerForm: {},
      SellBlockData: SellBlockData,
      developers: JSON.parse(sessionStorage.getItem('userInfo')).type,
      disabledDates: {
        from: new Date(),
      },
    }
  },
  computed: {
    rules () {
      var checkBuyerName = (rule, value, callback) => {
        const reg = /[a-z]/
        if (reg.test(value)) {
          return callback(new Error('Please input buyer namer in CAPITAL LETTERS.'));
        } else {
          callback();
        }
        // if (reg.test(value)) {
        //   return callback(new Error('年龄不能为空'));
        // }
      };
      let blurArr = [
        'buyerName',
        'buyerMobile',
        'buyerEmail',
        'nationality',
        'nricPassport',
      ]
      let changeArr = [
        'customerType',
        'dateOfBirth',
        'gender',
        'countryCallingCode',
      ]
      return {
        ...setRulesData('blur', blurArr),
        ...{ buyerName: [{ validator: checkBuyerName, trigger: 'change' }] },
        ...setRulesData('change', changeArr),
      }
    },
  },
  watch: {
    buyFom (val) {
      this.buyerForm = val
    },
  },
  methods: {
    addDataFn () {
      this.$refs['form_buyser'].validate((valid) => {
        if (valid) {
          if (this.buyerForm.dateOfBirth) {
            let dateOfBirth = this.$dateFormatNoTime(
              this.buyerForm.dateOfBirth
            ).split('-')
            let newDate = this.$todayFormat().split('-')

            if (!this.computeNumber(newDate, dateOfBirth)) {
              this.$notify.error({
                title: 'Error',
                message: 'Buyers must not be younger than 21',
              })
              return false
            }
          }

          this.$emit('EditSuccess', this.buyerForm)
          this.show = false
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    closedForm () {
      this.buyerForm = {}
    },
    computeNumber (newDate, oldDate) {
      let year = newDate[0] - oldDate[0]
      if (year > 21) {
        return true // 年份大于21 true
      } else {
        if (year == 21) {
          // 年份等于21

          if (newDate[1] > oldDate[1]) {
            // 年份等于21，月份大于。true
            return true
          } else {
            if (newDate[1] == oldDate[1]) {
              // 年份等于21，月份等于

              if (newDate[2] >= oldDate[2]) {
                // 年份等于21，月份等于，天数大于 true
                return true
              } else {
                // 年份等于21，月份等于，天数小于等于 false
                return false
              }
            } else {
              // 月份小于， false
              return false
            }
          }
        } else {
          // 年份小于 , false
          return false
        }
      }
    },
  },
}
</script>

<style lang="less">
.AddBuyerPop_box {
  height: 550px;
  overflow-y: scroll;
  padding: 15px;
  .buyerFormDatePicker {
    .DatePickerInputClass {
      width: 100%;
      height: 28px;
      padding: 0 15px;
      outline: none;
      border: 1px solid #dcdfe6;
      color: #606266;
      border-radius: 4px;
      transition: border-color 0.2s cubic-bezier(0.645, 0.045, 0.355, 1);
      &:focus {
        border: 1px solid #409eff;
      }
      &:hover {
        border: 1px solid #b8babe;
      }
    }
    .cell {
      &.selected {
        background: #409eff;
        color: #fff;
        &:hover {
          background: #409eff;
        }

        &.highlighted {
          background: #409eff;
        }
      }
    }
  }
}
</style>