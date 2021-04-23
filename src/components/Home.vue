<template>
  <div>
    <div class="container">
      <h1 class="text-center">Bank Information List</h1>
       <b-button
                style="width:100%;margin:2px"
                type="button"
                @click="bank_account_show(item)"
                class="btn-primary"
                v-b-modal.modal-1
                >Add New</b-button
              >
      <table class="table">
        <thead>
          <tr>
            <th>SL</th>
            <th>Account Name</th>
            <th>Bank</th>
            <th>Account No</th>
            <th>Branch</th>
            <th>Account Type</th>
            <th>Swift Code</th>
            <th>Route No</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in bank_accounts" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ item.account_name }}</td>
            <td>{{ item.bank_name.name }}</td>
            <td>{{ item.account_no }}</td>
            <td>{{ item.branch }}</td>
            <td v-if="item.account_type == 1">Saving Account</td>
            <td v-if="item.account_type == 2">Current</td>
            <td v-if="item.account_type == 3">Joint Account</td>
            <td>{{ item.swift_code }}</td>
            <td>{{ item.route_no }}</td>
            <td>
              <b-button
                style="width:100%;margin:2px"
                type="button"
                @click="bank_account_show(item)"
                class="btn-success"
                v-b-modal.modal-1
                >Edit</b-button
              >
              <button style="width:100%"  type="button" class="btn-danger" @click="deleteInfo(item.id)">
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div>
      <b-modal id="modal-1" title="Bank Information">
        <ul v-if='error' class="bg-danger">
            <li v-for='(er,errorind) in error' v-bind:key='errorind'>{{er[0]}}</li>
          </ul>
        <form>
          <div class="form-group">
            <label for="account_name">Account Name</label>
            <input
              type="text"
              class="form-control"
              id="account_name"
              v-model="account_name"
              placeholder="Enter Account Name"
            />
            <input type="hidden" name="id" v-model="id" />
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>
          <div class="form-group">
            <label for="financial_organization_id">Bank</label>
            <select
              name="financial_organization_id"
              class="form-control"
              v-model="financial_organization_id"
              id="financial_organization_id"
            >
              <option value="">select Bank</option>
              <option
                v-for="(financial_org, indexa) in financial_organization"
                :key="indexa"
                :value="financial_org.id"
                :title="financial_org.name"
              >
                {{ financial_org.name }}
              </option>
            </select>
          </div>
          <div class="form-group">
            <label for="branch">Branch</label>
            <input
              type="text"
              class="form-control"
              id="branch"
              v-model="branch"
              placeholder="Enter Branch Name"
            />
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>
          <div class="form-group">
            <label for="account_no">Account No</label>
            <input
              type="text"
              class="form-control"
              id="account_no"
              v-model="account_no"
              placeholder="Enter Account No"
            />
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>
          <div class="form-group">
            <label for="store_id">Store Id</label>
            <input
              type="text"
              class="form-control"
              id="store_id"
              v-model="store_id"
              placeholder="Enter Store Id"
            />
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>
          <div class="form-group">
            <label for="account_type">Account Type</label>
            <select
              name="account_type"
              class="form-control"
              v-model="account_type"
              id="account_type"
            >
              <option value=''>select Account Type</option>
              <option
                v-for="(accounttype, typeIndex) in account_types"
                :key="typeIndex"
                :value="accounttype.id"
                :title="accounttype.name"
              >
                {{ accounttype.name }}
              </option>
            </select>
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>
          <div class="form-group">
            <label for="swift_code">Swift Code</label>
            <input
              type="text"
              class="form-control"
              id="swift_code"
              v-model="swift_code"
              placeholder="Enter Swift Code"
            />
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>
          <div class="form-group">
            <label for="route_no">Route No</label>
            <input
              type="text"
              class="form-control"
              id="route_no"
              v-model="route_no"
              placeholder="Enter Swift Code"
            />
            <small id="emailHelp" class="form-text text-muted"></small>
          </div>

          <button
            type="submit"
            @click.prevent="saveBankInformation"
            class="btn btn-primary pull-right"
          >
            Save
          </button>
        </form>
      </b-modal>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Home",
  props: ["user"],
  data() {
    return {
      bank_accounts: [],
      financial_organization: [],
      account_types: [
        { id: 1, name: "Saving Account" },
        { id: 2, name: "Current Account" },
        { id: 3, name: "Joint Account" }
      ],
      account_name: "",
      financial_organization_id: "",
      branch: "",
      account_type: "",
      swift_code: "",
      route_no: "",
      account_no: "",
      store_id: "",
      id: "",
      account_name_error: "",
      financial_organization_id_error: "",
      branch_error: "",
      account_type_error: "",
      swift_code_error: "",
      route_no_error: "",
      account_no_error: "",
      store_id_error: "",
      item:{},
      error:null,
    };
  },
  async created() {
    const response = await axios.get("bank-account");
    this.bank_accounts = response.data.bank;
    this.financial_organization = response.data.forganization;
    console.log(response);
  },
  methods: {
    bank_account_show(item) {
      this.error=null;
      console.log(item);
      this.account_name = item.account_name;
      this.financial_organization_id = item.financial_organization_id;
      this.branch = item.branch;
      this.account_type = item.account_type;
      this.swift_code = item.swift_code;
      this.route_no = item.route_no;
      this.id = item.id;
      this.account_no=item.account_no;
      this.store_id=item.store_id;
    },

    async saveBankInformation() {

      const response = await axios.post("bank-account", {
        account_name: this.account_name,
        financial_organization_id: this.financial_organization_id,
        branch: this.branch,
        account_type: this.account_type,
        swift_code: this.swift_code,
        route_no: this.route_no,
        id:this.id,
        account_no:this.account_no,
        store_id:this.store_id,
      });
       console.log(response);
       if (response.status == 200 && response.data.error != undefined) {
        this.allInformation();
       }
       if (response.data.error) {
        this.error=response.data.error;
       }
       
    },
    async allInformation(){
      const response = await axios.get("bank-account");
      this.bank_accounts = response.data.bank;
      this.financial_organization = response.data.forganization;
      console.log(response);
    },
   async deleteInfo(id){
    if(confirm("Do you really want to delete?")){
      const response = await axios.delete(`bank-account/${id}`)
      console.log(response);
      if (response.status == 200) {
        let i = this.bank_accounts.map(item => item.id).indexOf(id); // find index of your object
        this.bank_accounts.splice(i, 1)
      }
        
      }
    }

  }
};
</script>
