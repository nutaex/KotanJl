<template>
  <div class="settings_wrapper">
    <div class="head">
      <el-row>
        <el-col :span="12" class="el_col_name">
          <div>{{$t('settings.settings')}}</div>
        </el-col>
        <el-col :span="12" style="text-align:right">
          <el-button :disabled="self == 0" size="mini" @click="saveSetting">{{$t('settings.update')}}</el-button>
          <el-button :disabled="self == 0" size="mini">{{$t('settings.cancel')}}</el-button>
        </el-col>
      </el-row>
    </div>
    <div class="setting_content">
      <el-form :inline="true" class="demo-form-inline form" label-width="350px" label-position="left" size="small">
        <el-alert style="padding:8px 0;margin-bottom:10px" title="Project Setting" type="info" :closable="false"></el-alert>
        <div style="padding:10px; text-align: center">
          <el-row>
            <el-col :span="6">
              <el-checkbox v-model="settingForm.showBroke" label="Co-Broke" border></el-checkbox>
            </el-col>
            <el-col :span="6">
              <el-checkbox v-model="settingForm.soldApprove" label="Sales approval" border></el-checkbox>
            </el-col>
            <el-col :span="6">
              <el-checkbox v-model="settingForm.showAvailable" label="Show Available" border></el-checkbox>
            </el-col>
            <el-col :span="6">
              <el-checkbox v-model="settingForm.launchStatus" label="OpenedDealMsg" border></el-checkbox>
            </el-col>
          </el-row>
          <!-- <el-checkbox v-model="checked3" label="备选项1" border></el-checkbox>
          <el-checkbox v-model="checked4" label="备选项2" border></el-checkbox>-->
        </div>
        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('settings.UnitInterest')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.InterestExpirationTime')">
                <!-- <el-date-picker class="width_300px" v-model="settingForm.interestExpirationTime" type="datetime" value-format="yyyy-MM-dd hh:mm:ss"></el-date-picker> -->
                <el-date-picker class="width_300px" v-model="settingForm.interestExpirationTime" type="datetime" value-format="timestamp"></el-date-picker>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.MaxInterestPerUserUnit')">
                <el-input class="width_300px" v-model="settingForm.maxInterestPerUserUnit"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.AllowInterestSoldUnit')">
                <el-checkbox v-model="settingForm.allowInterestSoldUnit" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
        </div>

        <el-alert style="padding:8px 0;margin-bottom:10px" title="Book Unit" type="info" :closable="false"></el-alert>
        <div class="div_padding_x">
          If the time limit expire, the unit will revert to available for sales status
          <el-row>
            <el-col :span="12">
              <el-form-item label="Online Booking Time Limit">
                <!-- <el-date-picker class="width_300px" v-model="settingForm.interestExpirationTime" type="datetime" value-format="yyyy-MM-dd hh:mm:ss"></el-date-picker> -->
                <el-radio v-model="radio" label="1">20min（System Default）</el-radio>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item>
                <el-radio v-model="radio" label="2">
                  Custom
                  <el-input class="width_300px" v-model="bookTime"></el-input>
                </el-radio>
              </el-form-item>
            </el-col>
          </el-row>
        </div>

        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('settings.unitCustomFieldLabels')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.areaLabel')">
                <el-input class="width_300px" v-model="settingForm.areaLabel"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField1')">
                <el-input class="width_300px" v-model="settingForm.custom1Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField2')">
                <el-input class="width_300px" v-model="settingForm.custom2Label"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField3')">
                <el-input class="width_300px" v-model="settingForm.custom3Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField4')">
                <el-input class="width_300px" v-model="settingForm.custom4Label"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField5')">
                <el-input class="width_300px" v-model="settingForm.custom5Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField6')">
                <el-input class="width_300px" v-model="settingForm.custom6Label"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField7')">
                <el-input class="width_300px" v-model="settingForm.custom7Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField8')">
                <el-input class="width_300px" v-model="settingForm.custom8Label"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField9')">
                <el-input class="width_300px" v-model="settingForm.custom9Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.customField10')">
                <el-input class="width_300px" v-model="settingForm.custom10Label"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </div>
        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('settings.unitPriceSettings')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x" style="border-bottom:1px solid #dcdfe6">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.defaultTransactionPriceLabel')">
                <el-input class="width_300px" v-model="settingForm.price1Label"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price2Label')">
                <el-input class="width_300px" v-model="settingForm.price2Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price2CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price2UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price3Label')">
                <el-input class="width_300px" v-model="settingForm.price3Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price3CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price3UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price4Label')">
                <el-input class="width_300px" v-model="settingForm.price4Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price4CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price4UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price5Label')">
                <el-input class="width_300px" v-model="settingForm.price5Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price5CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price5UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price6Label')">
                <el-input class="width_300px" v-model="settingForm.price6Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price6CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price6UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price7Label')">
                <el-input class="width_300px" v-model="settingForm.price7Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price7CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price7UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price8Label')">
                <el-input class="width_300px" v-model="settingForm.price8Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price8CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price8UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price9Label')">
                <el-input class="width_300px" v-model="settingForm.price9Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price9CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price9UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price10Label')">
                <el-input class="width_300px" v-model="settingForm.price10Label"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.price10CanbeusedforTransaction')">
                <el-checkbox v-model="settingForm.price10UsedTrans" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.priceInstuction')">
                <el-input class="width_300px" v-model="settingForm.priceInstuction"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.numofDecimalPlaces')">
                <el-input class="width_300px" v-model="settingForm.numOfDecimalPlaces"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </div>
        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('settings.ReservationFormSettings')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x" style="border-bottom:1px solid #dcdfe6">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.NameRequired')">
                <el-checkbox v-model="settingForm.nameRequired" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.MobileRequired')">
                <el-checkbox v-model="settingForm.mobileRequired" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.EmailRequired')">
                <el-checkbox v-model="settingForm.emailRequired" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.CommentsRequired')">
                <el-checkbox v-model="settingForm.commentsRequired" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SPAStampLable')">
                <el-input class="width_300px" v-model="settingForm.spaStampLable"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.AllowSecondSalesRep')">
                <el-checkbox v-model="settingForm.allowSecondSalesRep" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.EnableDiscount')">
                <el-checkbox v-model="settingForm.enableDiscount" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.AllowDiscountEntry')">
                <el-input class="width_300px" v-model="settingForm.allowDiscountEntry"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.UnitPriceLabel')">
                <el-input class="width_300px" v-model="settingForm.unitPriceLabel"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.AdditionalPriceLabel')">
                <el-input class="width_300px" v-model="settingForm.additionalPriceLabel"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.TotalPriceLabel')">
                <el-input class="width_300px" v-model="settingForm.totalPriceLabel"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SPAPriceLabel')">
                <el-input class="width_300px" v-model="settingForm.spaPriceLabel"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.RequireJustificationtoCancel')">
                <el-checkbox v-model="settingForm.requireJustificationToCancel" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.Depositrequiredfor')">
                <el-select class="width_300px" v-model="settingForm.depositRequiredFor">
                  <el-option label="Pending Reservation" value="Pending Reservation"></el-option>
                  <el-option label="Reserved" value="Reserved"></el-option>
                  <el-option label="Sold" value="Sold"></el-option>
                </el-select>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.ShowAndStamp')">
                <el-checkbox v-model="settingForm.showStamp" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.DefaultDepositAmount')">
                <el-input class="width_300px" v-model="settingForm.defaultDepositAmount"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </div>
        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('settings.NotificationSettings')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x" style="border-bottom:1px solid #dcdfe6">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.EnableReserveNotificationEmail')">
                <el-checkbox v-model="notificationSet.reserve" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.ReserveNotificationEmail')">
                <el-checkbox v-model="notificationSet.documentsInReserve" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SPASignNotificationEmail')">
                <el-checkbox v-model="notificationSet.pendingSPASign" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.EnableSPASignNotificationEmail')">
                <el-checkbox v-model="notificationSet.spaSign" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.DocumentsinSPASign')">
                <el-checkbox v-model="notificationSet.documentsInSpaSign" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SendPreReservedReminder')">
                <el-checkbox v-model="notificationSet.preReserved" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.NumberofDaysforReminder')">
                <el-input class="width_300px" v-model="notificationSet.preReservedDays" :maxlength="5"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SendReservationReminder')">
                <el-checkbox v-model="notificationSet.reservation" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.NumberofDaysforReminder')">
                <el-input class="width_300px" v-model="notificationSet.reservationDays" :maxlength="5"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SendPendingSPASignReminder')">
                <el-checkbox v-model="notificationSet.sendPendingSpaSign" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.NumberofDaysforReminder')">
                <el-input class="width_300px" v-model="notificationSet.sendPendingSpaSignDays" :maxlength="5"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SendPendingSPAStampReminder')">
                <el-checkbox v-model="notificationSet.pendingSpaStamp" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.NumberofDaysforReminder')">
                <el-input class="width_300px" v-model="notificationSet.pendingSpaStampDays" :maxlength="5"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SendSoldDateReminder')">
                <el-checkbox v-model="notificationSet.soldDate" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.NumberofDaysforReminder')">
                <el-input class="width_300px" v-model="notificationSet.soldDateDays" :maxlength="5"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </div>
        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('settings.BookingReissueSettings')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x" style="border-bottom:1px solid #dcdfe6">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.AllowReissue')">
                <el-checkbox v-model="settingForm.allowReissue" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.MaxReissue')">
                <el-input class="width_300px" v-model="settingForm.maxReissue"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('settings.SectionHeader')">
                <el-input class="width_300px" v-model="settingForm.sectionHeader"></el-input>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('settings.ItemLabel')">
                <el-input class="width_300px" v-model="settingForm.itemLabel"></el-input>
              </el-form-item>
            </el-col>
          </el-row>
        </div>
        <el-alert style="padding:8px 0;margin-bottom:10px" :title="$t('Price API')" type="info" :closable="false"></el-alert>
        <div class="div_padding_x" style="border-bottom:1px solid #dcdfe6">
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('Price 1')">
                <el-checkbox v-model="settingForm.price1Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('Price 2')">
                <el-checkbox v-model="settingForm.price2Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('Price 3')">
                <el-checkbox v-model="settingForm.price3Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('Price 4')">
                <el-checkbox v-model="settingForm.price4Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('Price 5')">
                <el-checkbox v-model="settingForm.price5Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('Price 6')">
                <el-checkbox v-model="settingForm.price6Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('Price 7')">
                <el-checkbox v-model="settingForm.price7Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('Price 8')">
                <el-checkbox v-model="settingForm.price8Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
          <el-row>
            <el-col :span="12">
              <el-form-item :label="$t('Price 9')">
                <el-checkbox v-model="settingForm.price9Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
            <el-col :span="12">
              <el-form-item :label="$t('Price 10')">
                <el-checkbox v-model="settingForm.price10Api" :true-label="0" :false-label="1"></el-checkbox>
              </el-form-item>
            </el-col>
          </el-row>
        </div>
      </el-form>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      self: JSON.parse(sessionStorage.getItem('projectDesc')).self,
      id: JSON.parse(sessionStorage.getItem('projectDesc') || '{}').id || '',
      radio: '1',
      bookTime: '',
      settingForm: {
        interestExpirationTime: '',
        maxInterestPerUserUnit: '',
        allowInterestSoldUnit: 1,
        areaLabel: '',
        custom1Label: '',
        custom2Label: '',
        custom3Label: '',
        custom4Label: '',
        custom5Label: '',
        custom6Label: '',
        custom7Label: '',
        custom8Label: '',
        custom9Label: '',
        custom10Label: '',
        price1Label: '',
        price2Label: '',
        price3Label: '',
        price4Label: '',
        price5Label: '',
        price6Label: '',
        price7Label: '',
        price8Label: '',
        price9Label: '',
        price10Label: '',
        price2UsedTrans: 1, //代表未勾选
        price3UsedTrans: 1,
        price4UsedTrans: 1,
        price5UsedTrans: 1,
        price6UsedTrans: 1,
        price7UsedTrans: 1,
        price8UsedTrans: 1,
        price9UsedTrans: 1,
        price10UsedTrans: 1,
        priceInstuction: '',
        numOfDecimalPlaces: '',
        nameRequired: '',
        mobileRequired: '',
        emailRequired: '',
        commentsRequired: '',
        spaStampLable: '',
        allowSecondSalesRep: '',
        enableDiscount: '',
        allowDiscountEntry: '',
        unitPriceLabel: '',
        additionalPriceLabel: '',
        totalPriceLabel: '',
        spaPriceLabel: '',
        requireJustificationToCancel: '',
        depositRequiredFor: 'Reserved',
        showStamp: '',
        defaultDepositAmount: '',
        allowReissue: '',
        maxReissue: '',
        sectionHeader: '',
        itemLabel: '',
        showBroke: 0,
        soldApprove: 0,
        showAvailable: 0,
        launchStatus: 0,
        price1Api: 1, //代表未勾选
        price2Api: 1,
        price3Api: 1,
        price4Api: 1,
        price5Api: 1,
        price6Api: 1,
        price7Api: 1,
        price8Api: 1,
        price9Api: 1,
        price10Api: 1
      },
      notificationSet: {
        reserve: '',
        documentsInReserve: '',
        pendingSPASign: '',
        spaSign: '',
        documentsInSpaSign: '',
        preReserved: '',
        preReservedDays: '',
        reservation: '',
        reservationDays: '',
        sendPendingSpaSign: '',
        sendPendingSpaSignDays: '',
        pendingSpaStamp: '',
        pendingSpaStampDays: '',
        soldDate: '',
        soldDateDays: ''
      },
      tableDataInit: -1,
      brokeList: [], //经纪公司列表

      noBrokeOfProjectList: [], // 未关联经纪公司
      brokeOfProjectList: [], //项目关联的经纪公司列表
      checkedBrokes: [], //选中的经纪公司
      brokeOfProjectNum: 0,
      companyId: '',
      defaultCommission: '',
      commissionListId: '',
      isEdit: false,
      isUpdataDisabled: false
    }
  },
  mounted () {
    if (this.id) {
      this.getSetting()
    }
  },
  methods: {
    getSetting () {
      //查询设置
      this.$Geting(this.$api.queryProjectSet, { projectId: this.id }).then(
        res => {
          if (res.code == 0) {
            if (!res.datas.projectSet) {
              return
            }
            this.settingForm = res.datas.projectSet
            this.settingForm.showBroke = !!res.datas.projectSet.showBroke
            this.settingForm.soldApprove = !!res.datas.projectSet.soldApprove
            this.settingForm.showAvailable = !!res.datas.projectSet
              .showAvailable
            this.settingForm.launchStatus = !!res.datas.projectSet.launchStatus
            this.notificationSet = res.datas.notificationSet || {}
            this.bookTime = res.datas.projectSet.bookTime
            this.radio = this.bookTime == 20 ? '1' : '2'
          } else {
            this.$notify.error({
              title: 'fail',
              message: res.msg
            })
            return false
          }
        }
      )
    },
    saveSetting () {
      // console.log(Number(this.settingForm.showBroke), Number(this.settingForm.soldApprove));
      this.settingForm.showBroke = Number(this.settingForm.showBroke)
      this.settingForm.soldApprove = Number(this.settingForm.soldApprove)
      this.settingForm.showAvailable = Number(this.settingForm.showAvailable)
      this.settingForm.launchStatus = Number(this.settingForm.launchStatus)

      //保存设置
      this.$Posting(this.$api.saveProjectSet, {
        projectId: this.id,
        ...this.settingForm,
        bookTime: this.radio == '1' ? 20 : this.bookTime
      }).then(res => {
        if (res.code == 0) {
          //保存SPA & Notification Settings
          this.$Posting(this.$api.saveSpaNotificationSettings, {
            projectId: this.id,
            ...this.notificationSet
          }).then(res => {
            if (res.code == 0) {
              this.$notify.success({
                title: this.$t('alert.alert_success_title'),
                message: this.$t('alert.operate_success_title')
              })
              this.getSetting()
            } else {
              this.$notify.error({
                title: 'fail',
                message: res.msg
              })
              return false
            }
          })
        } else {
          this.$notify.error({
            title: 'fail',
            message: res.msg
          })
          return false
        }
      })
    }
  }
}
</script>
<style lang="less">
.settings_wrapper {
  background-color: #fff;
  height: 100%;
  position: relative;
  overflow: hidden;
  .head {
    height: 62px;
    position: absolute;
    top: 0;
    width: 100%;
    border-bottom: 1px solid #dcdfe6;
    border-top: 1px solid #dcdfe6;
    padding: 15px 30px;
    .el_col_name {
      div {
        padding: 4px 0;
      }
    }
  }
  .setting_content {
    position: absolute;
    top: 62px;
    bottom: 0;
    width: 100%;
    overflow: auto;
    padding: 15px 30px;
    .el-alert__title {
      font-size: 14px !important;
    }
  }
  .div_padding_x {
    padding: 0 30px;
  }
  .row_header {
    height: 62px;
    padding: 15px 0;
    .col_text {
      padding: 4px 0;
    }
    .col_button {
      text-align: right;
    }
  }
}
</style>


