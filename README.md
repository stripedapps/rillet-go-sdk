# Rillet Go SDK

Go client library for the [Rillet Accounting API](https://api.rillet.com). Covers contracts, invoices, bills, payments, journal entries, customers, vendors, reports, webhooks, and more.

This client is generated from the Rillet OpenAPI spec using [OpenAPI Generator](https://openapi-generator.tech). Do not edit the generated files directly — regenerate from the spec instead.

- API version: v3.0
- Package version: 1.0.0
- Generator version: 7.13.0

## Installation

```sh
go get github.com/stripedapps/rillet-go-sdk
```

Import in your code:

```go
import openapi "github.com/stripedapps/rillet-go-sdk"
```

## Quick start

```go
package main

import (
	"context"
	"fmt"
	"log"

	openapi "github.com/stripedapps/rillet-go-sdk"
)

func main() {
	cfg := openapi.NewConfiguration()
	client := openapi.NewAPIClient(cfg)

	ctx := context.WithValue(context.Background(), openapi.ContextAccessToken, "YOUR_BEARER_TOKEN")

	customers, _, err := client.CustomersAPI.ListAllCustomers(ctx).Execute()
	if err != nil {
		log.Fatal(err)
	}
	fmt.Printf("%d customers\n", len(customers.GetData()))
}
```

To use a proxy, set the environment variable `HTTP_PROXY`:

```go
os.Setenv("HTTP_PROXY", "http://proxy_name:proxy_port")
```

## Configuration of Server URL

Default configuration comes with `Servers` field that contains server objects as defined in the OpenAPI specification.

### Select Server Configuration

For using other server than the one defined on index 0 set context value `openapi.ContextServerIndex` of type `int`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextServerIndex, 1)
```

### Templated Server URL

Templated server URL is formatted using default variables from configuration or from context value `openapi.ContextServerVariables` of type `map[string]string`.

```go
ctx := context.WithValue(context.Background(), openapi.ContextServerVariables, map[string]string{
	"basePath": "v2",
})
```

Note, enum values are always validated and all unused variables are silently ignored.

### URLs Configuration per Operation

Each operation can use different server URL defined using `OperationServers` map in the `Configuration`.
An operation is uniquely identified by `"{classname}Service.{nickname}"` string.
Similar rules for overriding default operation server index and variables applies by using `openapi.ContextOperationServerIndices` and `openapi.ContextOperationServerVariables` context maps.

```go
ctx := context.WithValue(context.Background(), openapi.ContextOperationServerIndices, map[string]int{
	"{classname}Service.{nickname}": 2,
})
ctx = context.WithValue(context.Background(), openapi.ContextOperationServerVariables, map[string]map[string]string{
	"{classname}Service.{nickname}": {
		"port": "8443",
	},
})
```

## Documentation for API Endpoints

All URIs are relative to *https://api.rillet.com*

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*APIKeyAPI* | [**GetApiKeyInformation**](docs/APIKeyAPI.md#getapikeyinformation) | **Get** /api-key | Gets API key information
*BankAccountsAPI* | [**CreateABankAccount**](docs/BankAccountsAPI.md#createabankaccount) | **Post** /bank-accounts | Creates a bank account
*BankAccountsAPI* | [**DeleteABankAccount**](docs/BankAccountsAPI.md#deleteabankaccount) | **Delete** /bank-accounts/{bank_account_id} | Deletes a bank account
*BankAccountsAPI* | [**ListAllBankAccounts**](docs/BankAccountsAPI.md#listallbankaccounts) | **Get** /bank-accounts | Lists all bank accounts
*BankAccountsAPI* | [**RetrieveABankAccount**](docs/BankAccountsAPI.md#retrieveabankaccount) | **Get** /bank-accounts/{bank_account_id} | Retrieves a bank account
*BankTransactionsAPI* | [**CreateABankTransaction**](docs/BankTransactionsAPI.md#createabanktransaction) | **Post** /bank-transactions | Creates a bank transaction
*BankTransactionsAPI* | [**DeleteABankTransaction**](docs/BankTransactionsAPI.md#deleteabanktransaction) | **Delete** /bank-transactions/{bank_transaction_id} | Deletes a bank transaction
*BankTransactionsAPI* | [**ListAllBankTransactions**](docs/BankTransactionsAPI.md#listallbanktransactions) | **Get** /bank-transactions | Lists all bank transactions
*BankTransactionsAPI* | [**RetrieveABankTransaction**](docs/BankTransactionsAPI.md#retrieveabanktransaction) | **Get** /bank-transactions/{bank_transaction_id} | Retrieves a bank transaction
*BankTransactionsAPI* | [**UpdateABankTransaction**](docs/BankTransactionsAPI.md#updateabanktransaction) | **Put** /bank-transactions/{bank_transaction_id} | Updates a bank transaction
*BillPaymentsAPI* | [**CreateABillPayment**](docs/BillPaymentsAPI.md#createabillpayment) | **Post** /bills/{bill_id}/payments | Creates a bill payment
*BillPaymentsAPI* | [**DeleteABillPayment**](docs/BillPaymentsAPI.md#deleteabillpayment) | **Delete** /bills/{bill_id}/payments/{payment_id} | Deletes a bill payment
*BillPaymentsAPI* | [**ListBillPayments**](docs/BillPaymentsAPI.md#listbillpayments) | **Get** /bills/{bill_id}/payments | Lists bill payments
*BillsAPI* | [**CreateABill**](docs/BillsAPI.md#createabill) | **Post** /bills | Creates a bill
*BillsAPI* | [**DeleteABill**](docs/BillsAPI.md#deleteabill) | **Delete** /bills/{bill_id} | Deletes a bill
*BillsAPI* | [**ListAllBills**](docs/BillsAPI.md#listallbills) | **Get** /bills | Lists all bills
*BillsAPI* | [**RetrieveABill**](docs/BillsAPI.md#retrieveabill) | **Get** /bills/{bill_id} | Retrieves a bill
*BillsAPI* | [**UpdateABill**](docs/BillsAPI.md#updateabill) | **Put** /bills/{bill_id} | Updates a bill
*BillsAPI* | [**UploadDocument**](docs/BillsAPI.md#uploaddocument) | **Post** /bills/{bill_id} | Uploads a document
*BooksPeriodsAPI* | [**RetrieveLastBookClosedPeriod**](docs/BooksPeriodsAPI.md#retrievelastbookclosedperiod) | **Get** /books/periods/last-closed | Retrieves last book closed period
*ChargesAPI* | [**DeleteACharge**](docs/ChargesAPI.md#deleteacharge) | **Delete** /charges/{charge_id} | Deletes a charge
*ChargesAPI* | [**ListAllCharges**](docs/ChargesAPI.md#listallcharges) | **Get** /charges | Lists all charges
*ChargesAPI* | [**RetrieveACharge**](docs/ChargesAPI.md#retrieveacharge) | **Get** /charges/{charge_id} | Retrieves a charge
*ChartOfAccountsAPI* | [**ListAllAccounts**](docs/ChartOfAccountsAPI.md#listallaccounts) | **Get** /accounts | Lists all accounts
*ContractItemsAPI* | [**DeleteAUsageRecord**](docs/ContractItemsAPI.md#deleteausagerecord) | **Delete** /contract-items/{contract_item_id}/usage | Deletes a usage record
*ContractItemsAPI* | [**ListAllContractItemUsageRecords**](docs/ContractItemsAPI.md#listallcontractitemusagerecords) | **Get** /contract-items/{contract_item_id}/usage | Lists all contract item usage records
*ContractItemsAPI* | [**UpsertAUsageRecord**](docs/ContractItemsAPI.md#upsertausagerecord) | **Patch** /contract-items/{contract_item_id}/usage | Upserts a usage record
*ContractsAPI* | [**AmendAContract**](docs/ContractsAPI.md#amendacontract) | **Post** /contracts/{contract_id}/amendments | Amends a contract
*ContractsAPI* | [**CreateAContract**](docs/ContractsAPI.md#createacontract) | **Post** /contracts | Creates a contract
*ContractsAPI* | [**DeleteAContract**](docs/ContractsAPI.md#deleteacontract) | **Delete** /contracts/{contract_id} | Deletes a contract
*ContractsAPI* | [**EndAnOpenEndedContract**](docs/ContractsAPI.md#endanopenendedcontract) | **Put** /contracts/{contract_id}/end | Ends an open-ended contract
*ContractsAPI* | [**ListAllContracts**](docs/ContractsAPI.md#listallcontracts) | **Get** /contracts | Lists all contracts
*ContractsAPI* | [**PreviewContractAmendment**](docs/ContractsAPI.md#previewcontractamendment) | **Post** /contracts/{contract_id}/amendments/preview | Previews contract amendment
*ContractsAPI* | [**RetrieveAContract**](docs/ContractsAPI.md#retrieveacontract) | **Get** /contracts/{contract_id} | Retrieves a contract
*CreditMemosAPI* | [**CreateACreditMemo**](docs/CreditMemosAPI.md#createacreditmemo) | **Post** /credit-memos | Creates a credit memo
*CreditMemosAPI* | [**DeleteACreditMemo**](docs/CreditMemosAPI.md#deleteacreditmemo) | **Delete** /credit-memos/{credit_memo_id} | Deletes a credit memo
*CreditMemosAPI* | [**ListAllCreditMemos**](docs/CreditMemosAPI.md#listallcreditmemos) | **Get** /credit-memos | Lists all credit memos
*CreditMemosAPI* | [**RetrieveACreditMemo**](docs/CreditMemosAPI.md#retrieveacreditmemo) | **Get** /credit-memos/{credit_memo_id} | Retrieves a credit memo
*CreditMemosAPI* | [**UpdateACreditMemo**](docs/CreditMemosAPI.md#updateacreditmemo) | **Put** /credit-memos/{credit_memo_id} | Updates a credit memo
*CreditMemosAPI* | [**UpdateTaxesForACreditMemo**](docs/CreditMemosAPI.md#updatetaxesforacreditmemo) | **Post** /credit-memos/{credit_memo_id}/taxes | Updates credit memo taxes
*CustomerPaymentsAPI* | [**GetPaymentMethod**](docs/CustomerPaymentsAPI.md#getpaymentmethod) | **Get** /customers/{customer_id}/settings/payment | Gets payment method
*CustomerPaymentsAPI* | [**SetupAutoPayment**](docs/CustomerPaymentsAPI.md#setupautopayment) | **Post** /customers/{customer_id}/settings/payment | Sets up auto-payment
*CustomersAPI* | [**CreateACustomer**](docs/CustomersAPI.md#createacustomer) | **Post** /customers | Creates a customer
*CustomersAPI* | [**DeleteACustomer**](docs/CustomersAPI.md#deleteacustomer) | **Delete** /customers/{customer_id} | Deletes a customer
*CustomersAPI* | [**ListAllCustomers**](docs/CustomersAPI.md#listallcustomers) | **Get** /customers | Lists all customers
*CustomersAPI* | [**RetrieveACustomer**](docs/CustomersAPI.md#retrieveacustomer) | **Get** /customers/{customer_id} | Retrieves a customer
*CustomersAPI* | [**UpdateACustomer**](docs/CustomersAPI.md#updateacustomer) | **Put** /customers/{customer_id} | Updates a customer
*FieldsAPI* | [**CreateField**](docs/FieldsAPI.md#createfield) | **Post** /fields | Creates a field
*FieldsAPI* | [**CreateFieldValue**](docs/FieldsAPI.md#createfieldvalue) | **Post** /fields/{id}/values | Creates a field value
*FieldsAPI* | [**DeleteFieldValue**](docs/FieldsAPI.md#deletefieldvalue) | **Delete** /fields/{fieldId}/values/{fieldValueId} | Deletes a field value
*FieldsAPI* | [**GetFields**](docs/FieldsAPI.md#getfields) | **Get** /fields | Gets custom fields
*FieldsAPI* | [**UpdateField**](docs/FieldsAPI.md#updatefield) | **Put** /fields/{id} | Updates a field
*FieldsAPI* | [**UpdateFieldValue**](docs/FieldsAPI.md#updatefieldvalue) | **Put** /fields/{fieldId}/values/{fieldValueId} | Updates a field value
*HealthAPI* | [**Health**](docs/HealthAPI.md#health) | **Get** /health | Returns service health
*InvoicePaymentsAPI* | [**CreateAnInvoicePayment**](docs/InvoicePaymentsAPI.md#createaninvoicepayment) | **Post** /invoices/{invoice_id}/payments | Creates an invoice payment
*InvoicePaymentsAPI* | [**ListAllInvoicePayments**](docs/InvoicePaymentsAPI.md#listallinvoicepayments) | **Get** /invoices/{invoice_id}/payments | Lists payments for a given invoice
*InvoicePaymentsAPI* | [**ListAllInvoicesPayments**](docs/InvoicePaymentsAPI.md#listallinvoicespayments) | **Get** /invoice-payments | Lists all invoice payments
*InvoicesAPI* | [**CreateAnInvoice**](docs/InvoicesAPI.md#createaninvoice) | **Post** /invoices | Creates an invoice
*InvoicesAPI* | [**DeleteAnInvoice**](docs/InvoicesAPI.md#deleteaninvoice) | **Delete** /invoices/{invoice_id} | Deletes an invoice
*InvoicesAPI* | [**ListAllInvoices**](docs/InvoicesAPI.md#listallinvoices) | **Get** /invoices | Lists all invoices
*InvoicesAPI* | [**RetrieveAnInvoice**](docs/InvoicesAPI.md#retrieveaninvoice) | **Get** /invoices/{invoice_id} | Retrieves an invoice
*InvoicesAPI* | [**UpdateAnInvoice**](docs/InvoicesAPI.md#updateaninvoice) | **Put** /invoices/{invoice_id} | Updates an invoice
*InvoicesAPI* | [**UpdateInvoiceSentStatus**](docs/InvoicesAPI.md#updateinvoicesentstatus) | **Put** /invoices/{invoice_id}/sent-status | Updates invoice sent status
*InvoicesAPI* | [**UpdateTaxesForAnInvoice**](docs/InvoicesAPI.md#updatetaxesforaninvoice) | **Post** /invoices/{invoice_id}/taxes | Updates invoice taxes
*JournalEntriesAPI* | [**CreateAJournalEntry**](docs/JournalEntriesAPI.md#createajournalentry) | **Post** /journal-entries | Creates a journal entry
*JournalEntriesAPI* | [**DeleteAJournalEntry**](docs/JournalEntriesAPI.md#deleteajournalentry) | **Delete** /journal-entries/{journal_entry_id} | Deletes a journal entry
*JournalEntriesAPI* | [**ListAllJournalEntries**](docs/JournalEntriesAPI.md#listalljournalentries) | **Get** /journal-entries | Lists all journal entries
*JournalEntriesAPI* | [**RetrieveAJournalEntry**](docs/JournalEntriesAPI.md#retrieveajournalentry) | **Get** /journal-entries/{journal_entry_id} | Retrieves a journal entry
*JournalEntriesAPI* | [**UpdateAJournalEntry**](docs/JournalEntriesAPI.md#updateajournalentry) | **Put** /journal-entries/{journal_entry_id} | Updates a journal entry
*OrganizationsAPI* | [**RetrieveAnOrganization**](docs/OrganizationsAPI.md#retrieveanorganization) | **Get** /organizations/self | Retrieves an organization
*ProductsAPI* | [**CreateAProduct**](docs/ProductsAPI.md#createaproduct) | **Post** /products | Creates a product
*ProductsAPI* | [**DeleteAProduct**](docs/ProductsAPI.md#deleteaproduct) | **Delete** /products/{product_id} | Deletes a product
*ProductsAPI* | [**ListAllProducts**](docs/ProductsAPI.md#listallproducts) | **Get** /products | Lists all products
*ProductsAPI* | [**RetrieveAProduct**](docs/ProductsAPI.md#retrieveaproduct) | **Get** /products/{product_id} | Retrieves a product
*ProductsAPI* | [**UpdateAProduct**](docs/ProductsAPI.md#updateaproduct) | **Put** /products/{product_id} | Updates a product
*ReimbursementsAPI* | [**DeleteAReimbursement**](docs/ReimbursementsAPI.md#deleteareimbursement) | **Delete** /reimbursements/{reimbursement_id} | Deletes a reimbursement
*ReimbursementsAPI* | [**ListAllReimbursements**](docs/ReimbursementsAPI.md#listallreimbursements) | **Get** /reimbursements | Lists all reimbursements
*ReimbursementsAPI* | [**RetrieveAReimbursement**](docs/ReimbursementsAPI.md#retrieveareimbursement) | **Get** /reimbursements/{reimbursement_id} | Retrieves a reimbursement
*ReportsAPI* | [**ListReportsJournalEntries**](docs/ReportsAPI.md#listreportsjournalentries) | **Get** /reports/journal-entries | Lists journal entries with reporting currency amounts
*ReportsAPI* | [**RetrieveBalanceSheetReport**](docs/ReportsAPI.md#retrievebalancesheetreport) | **Get** /reports/balance-sheet | Retrieves balance sheet report
*ReportsAPI* | [**RetrieveCashFlowStatementReport**](docs/ReportsAPI.md#retrievecashflowstatementreport) | **Get** /reports/cash-flow-statement | Retrieves cash flow statement report
*ReportsAPI* | [**RetrieveExecutivePlReport**](docs/ReportsAPI.md#retrieveexecutiveplreport) | **Get** /reports/executive-pl | Retrieves executive P&amp;L report
*ReportsAPI* | [**RetrieveIncomeStatementReport**](docs/ReportsAPI.md#retrieveincomestatementreport) | **Get** /reports/income-statement | Retrieves income statement report
*ReportsAPI* | [**RetrieveTrialBalanceReport**](docs/ReportsAPI.md#retrievetrialbalancereport) | **Get** /reports/trial-balance | Retrieves trial balance report
*ReportsAPI* | [**RetrieveWaterfallReport**](docs/ReportsAPI.md#retrievewaterfallreport) | **Get** /reports/arr-waterfall | Retrieves ARR waterfall report
*SubsidiariesAPI* | [**ListAllSubsidiaries**](docs/SubsidiariesAPI.md#listallsubsidiaries) | **Get** /subsidiaries | Lists all subsidiaries
*SubsidiariesAPI* | [**RetrieveASubsidiary**](docs/SubsidiariesAPI.md#retrieveasubsidiary) | **Get** /subsidiaries/{subsidiary_id} | Retrieves a subsidiary
*TaxRatesAPI* | [**ListAllTaxRates**](docs/TaxRatesAPI.md#listalltaxrates) | **Get** /tax-rates | Lists all tax rates
*VendorCreditApplicationsAPI* | [**ApplyVendorCredit**](docs/VendorCreditApplicationsAPI.md#applyvendorcredit) | **Post** /vendor-credits/{vendor_credit_id}/applications | Applies a vendor credit to bills
*VendorCreditsAPI* | [**CreateAVendorCredit**](docs/VendorCreditsAPI.md#createavendorcredit) | **Post** /vendor-credits | Creates a vendor credit
*VendorCreditsAPI* | [**DeleteAVendorCredit**](docs/VendorCreditsAPI.md#deleteavendorcredit) | **Delete** /vendor-credits/{vendor_credit_id} | Deletes a vendor credit
*VendorCreditsAPI* | [**ListAllVendorCredits**](docs/VendorCreditsAPI.md#listallvendorcredits) | **Get** /vendor-credits | Lists all vendor credits
*VendorCreditsAPI* | [**RetrieveAVendorCredit**](docs/VendorCreditsAPI.md#retrieveavendorcredit) | **Get** /vendor-credits/{vendor_credit_id} | Retrieves a vendor credit
*VendorCreditsAPI* | [**UpdateAVendorCredit**](docs/VendorCreditsAPI.md#updateavendorcredit) | **Put** /vendor-credits/{vendor_credit_id} | Updates a vendor credit
*VendorsAPI* | [**CreateAVendor**](docs/VendorsAPI.md#createavendor) | **Post** /vendors | Creates a vendor
*VendorsAPI* | [**DeleteAVendor**](docs/VendorsAPI.md#deleteavendor) | **Delete** /vendors/{vendor_id} | Deletes a vendor
*VendorsAPI* | [**ListAllVendors**](docs/VendorsAPI.md#listallvendors) | **Get** /vendors | Lists all vendors
*VendorsAPI* | [**RetrieveAVendor**](docs/VendorsAPI.md#retrieveavendor) | **Get** /vendors/{vendor_id} | Retrieves a vendor
*VendorsAPI* | [**UpdateAVendor**](docs/VendorsAPI.md#updateavendor) | **Put** /vendors/{vendor_id} | Updates a vendor


## Documentation For Models

 - [Account](docs/Account.md)
 - [Address](docs/Address.md)
 - [AmendContractRequest](docs/AmendContractRequest.md)
 - [AmendFullContractItemRequest](docs/AmendFullContractItemRequest.md)
 - [AmendFullContractRequest](docs/AmendFullContractRequest.md)
 - [AmendRevenueRecognitionOnlyContractRequest](docs/AmendRevenueRecognitionOnlyContractRequest.md)
 - [AmendRevenueRecognitionOnlyContractRequestItemsInner](docs/AmendRevenueRecognitionOnlyContractRequestItemsInner.md)
 - [AmendmentEffectiveFrom](docs/AmendmentEffectiveFrom.md)
 - [AmountDiscount](docs/AmountDiscount.md)
 - [ApplyVendorCreditRequest](docs/ApplyVendorCreditRequest.md)
 - [BalanceSheetReport](docs/BalanceSheetReport.md)
 - [BankAccount](docs/BankAccount.md)
 - [BankAccountStatus](docs/BankAccountStatus.md)
 - [BankTransaction](docs/BankTransaction.md)
 - [BaseVendorCreditRequest](docs/BaseVendorCreditRequest.md)
 - [Bill](docs/Bill.md)
 - [BillItem](docs/BillItem.md)
 - [BillItemRequest](docs/BillItemRequest.md)
 - [BillPayment](docs/BillPayment.md)
 - [BillPaymentRequest](docs/BillPaymentRequest.md)
 - [BillStatus](docs/BillStatus.md)
 - [BillingScheme](docs/BillingScheme.md)
 - [Book](docs/Book.md)
 - [Breakdown](docs/Breakdown.md)
 - [BreakdownBalance](docs/BreakdownBalance.md)
 - [BreakdownMargin](docs/BreakdownMargin.md)
 - [CalendarPeriod](docs/CalendarPeriod.md)
 - [CashFlowItem](docs/CashFlowItem.md)
 - [CashFlowSection](docs/CashFlowSection.md)
 - [CashFlowStatementReport](docs/CashFlowStatementReport.md)
 - [Charge](docs/Charge.md)
 - [ChargeItem](docs/ChargeItem.md)
 - [ChargeItemRequest](docs/ChargeItemRequest.md)
 - [ChargePayment](docs/ChargePayment.md)
 - [ChargePaymentRequest](docs/ChargePaymentRequest.md)
 - [ChargeRequest](docs/ChargeRequest.md)
 - [ChargeStatus](docs/ChargeStatus.md)
 - [CommitInvoiceTaxesRequest](docs/CommitInvoiceTaxesRequest.md)
 - [Contract](docs/Contract.md)
 - [ContractInvoice](docs/ContractInvoice.md)
 - [ContractItem](docs/ContractItem.md)
 - [ContractItemRequest](docs/ContractItemRequest.md)
 - [ContractScope](docs/ContractScope.md)
 - [ContractStatus](docs/ContractStatus.md)
 - [CreateBankAccountRequest](docs/CreateBankAccountRequest.md)
 - [CreateBankTransactionRequest](docs/CreateBankTransactionRequest.md)
 - [CreateBillRequest](docs/CreateBillRequest.md)
 - [CreateContractRequest](docs/CreateContractRequest.md)
 - [CreateCreditMemoItemRequest](docs/CreateCreditMemoItemRequest.md)
 - [CreateCreditMemoRequest](docs/CreateCreditMemoRequest.md)
 - [CreateFieldRequest](docs/CreateFieldRequest.md)
 - [CreateFieldRequestValue](docs/CreateFieldRequestValue.md)
 - [CreateFieldValueRequest](docs/CreateFieldValueRequest.md)
 - [CreateFullContractRequest](docs/CreateFullContractRequest.md)
 - [CreateFullInvoiceItemRequest](docs/CreateFullInvoiceItemRequest.md)
 - [CreateFullInvoiceRequest](docs/CreateFullInvoiceRequest.md)
 - [CreateInvoiceRequest](docs/CreateInvoiceRequest.md)
 - [CreateJournalEntryRequest](docs/CreateJournalEntryRequest.md)
 - [CreateRevenueRecognitionOnlyContractRequest](docs/CreateRevenueRecognitionOnlyContractRequest.md)
 - [CreateRevenueRecognitionOnlyInvoiceItemRequest](docs/CreateRevenueRecognitionOnlyInvoiceItemRequest.md)
 - [CreateRevenueRecognitionOnlyInvoiceRequest](docs/CreateRevenueRecognitionOnlyInvoiceRequest.md)
 - [CreateVendorCreditRequest](docs/CreateVendorCreditRequest.md)
 - [CreditMemo](docs/CreditMemo.md)
 - [CreditMemoItem](docs/CreditMemoItem.md)
 - [CreditMemoItemPriceRequest](docs/CreditMemoItemPriceRequest.md)
 - [Customer](docs/Customer.md)
 - [CustomerEmail](docs/CustomerEmail.md)
 - [CustomerPaymentMethod](docs/CustomerPaymentMethod.md)
 - [CustomerRequest](docs/CustomerRequest.md)
 - [CustomerRevenue](docs/CustomerRevenue.md)
 - [Discount](docs/Discount.md)
 - [EndOpenEndedContractRequest](docs/EndOpenEndedContractRequest.md)
 - [Error](docs/Error.md)
 - [ExchangeRate](docs/ExchangeRate.md)
 - [ExecutivePLItem](docs/ExecutivePLItem.md)
 - [ExecutivePLReport](docs/ExecutivePLReport.md)
 - [ExecutivePLSection](docs/ExecutivePLSection.md)
 - [ExpandedContract](docs/ExpandedContract.md)
 - [ExpenseTaxRate](docs/ExpenseTaxRate.md)
 - [ExternalReference](docs/ExternalReference.md)
 - [Field](docs/Field.md)
 - [FieldAssignmentsInner](docs/FieldAssignmentsInner.md)
 - [FieldSettings](docs/FieldSettings.md)
 - [FieldSettingsMap](docs/FieldSettingsMap.md)
 - [FieldValue](docs/FieldValue.md)
 - [FieldsResponse](docs/FieldsResponse.md)
 - [FixedPrice](docs/FixedPrice.md)
 - [FixedRecurringPrice](docs/FixedRecurringPrice.md)
 - [IncomeStatementReport](docs/IncomeStatementReport.md)
 - [Invoice](docs/Invoice.md)
 - [InvoiceItem](docs/InvoiceItem.md)
 - [InvoiceItemPriceRequest](docs/InvoiceItemPriceRequest.md)
 - [InvoicePayment](docs/InvoicePayment.md)
 - [InvoicePaymentRequest](docs/InvoicePaymentRequest.md)
 - [InvoiceSchedule](docs/InvoiceSchedule.md)
 - [InvoiceScheduleInvoice](docs/InvoiceScheduleInvoice.md)
 - [InvoiceScheduleInvoiceItem](docs/InvoiceScheduleInvoiceItem.md)
 - [InvoiceScope](docs/InvoiceScope.md)
 - [InvoiceStatus](docs/InvoiceStatus.md)
 - [Invoicing](docs/Invoicing.md)
 - [InvoicingBankAccount](docs/InvoicingBankAccount.md)
 - [ItemRevenue](docs/ItemRevenue.md)
 - [JournalEntry](docs/JournalEntry.md)
 - [JournalEntryItem](docs/JournalEntryItem.md)
 - [JournalEntryItemRequest](docs/JournalEntryItemRequest.md)
 - [JournalEntryRelatedEntity](docs/JournalEntryRelatedEntity.md)
 - [ListAllAccounts200Response](docs/ListAllAccounts200Response.md)
 - [ListAllBankAccounts200Response](docs/ListAllBankAccounts200Response.md)
 - [ListAllBankTransactions200Response](docs/ListAllBankTransactions200Response.md)
 - [ListAllBills200Response](docs/ListAllBills200Response.md)
 - [ListAllCharges200Response](docs/ListAllCharges200Response.md)
 - [ListAllContractItemUsageRecords200Response](docs/ListAllContractItemUsageRecords200Response.md)
 - [ListAllContracts200Response](docs/ListAllContracts200Response.md)
 - [ListAllCreditMemos200Response](docs/ListAllCreditMemos200Response.md)
 - [ListAllCustomers200Response](docs/ListAllCustomers200Response.md)
 - [ListAllInvoicePayments200Response](docs/ListAllInvoicePayments200Response.md)
 - [ListAllInvoices200Response](docs/ListAllInvoices200Response.md)
 - [ListAllInvoicesPayments200Response](docs/ListAllInvoicesPayments200Response.md)
 - [ListAllJournalEntries200Response](docs/ListAllJournalEntries200Response.md)
 - [ListAllProducts200Response](docs/ListAllProducts200Response.md)
 - [ListAllReimbursements200Response](docs/ListAllReimbursements200Response.md)
 - [ListAllSubsidiaries200Response](docs/ListAllSubsidiaries200Response.md)
 - [ListAllTaxRates200Response](docs/ListAllTaxRates200Response.md)
 - [ListAllVendorCredits200Response](docs/ListAllVendorCredits200Response.md)
 - [ListAllVendors200Response](docs/ListAllVendors200Response.md)
 - [ListBillPayments200Response](docs/ListBillPayments200Response.md)
 - [ListReportsJournalEntries200Response](docs/ListReportsJournalEntries200Response.md)
 - [MinimumCommitmentInvoicing](docs/MinimumCommitmentInvoicing.md)
 - [MinimumCommitmentInvoicingFrequency](docs/MinimumCommitmentInvoicingFrequency.md)
 - [MonetaryAmount](docs/MonetaryAmount.md)
 - [MonthlyInvoicing](docs/MonthlyInvoicing.md)
 - [MonthlyProratedInvoicing](docs/MonthlyProratedInvoicing.md)
 - [NamedCashFlowSection](docs/NamedCashFlowSection.md)
 - [NamedExecutivePLSection](docs/NamedExecutivePLSection.md)
 - [NamedReportSection](docs/NamedReportSection.md)
 - [OneTimePrice](docs/OneTimePrice.md)
 - [Organization](docs/Organization.md)
 - [OverageInvoicing](docs/OverageInvoicing.md)
 - [OverageMonthlyInvoicing](docs/OverageMonthlyInvoicing.md)
 - [OverageMonthlyProratedInvoicing](docs/OverageMonthlyProratedInvoicing.md)
 - [OverageQuarterlyInvoicing](docs/OverageQuarterlyInvoicing.md)
 - [OverageSemiAnnualInvoicing](docs/OverageSemiAnnualInvoicing.md)
 - [OverageYearlyInvoicing](docs/OverageYearlyInvoicing.md)
 - [Pagination](docs/Pagination.md)
 - [PaymentSetupResponse](docs/PaymentSetupResponse.md)
 - [PerUnitBilling](docs/PerUnitBilling.md)
 - [PercentageDiscount](docs/PercentageDiscount.md)
 - [PreviewContractAmendmentRequest](docs/PreviewContractAmendmentRequest.md)
 - [Price](docs/Price.md)
 - [Product](docs/Product.md)
 - [ProductRequest](docs/ProductRequest.md)
 - [QuarterlyInvoicing](docs/QuarterlyInvoicing.md)
 - [RecurringPrice](docs/RecurringPrice.md)
 - [Reimbursement](docs/Reimbursement.md)
 - [ReimbursementItem](docs/ReimbursementItem.md)
 - [ReimbursementItemRequest](docs/ReimbursementItemRequest.md)
 - [ReimbursementPayment](docs/ReimbursementPayment.md)
 - [ReimbursementPaymentRequest](docs/ReimbursementPaymentRequest.md)
 - [ReimbursementRequest](docs/ReimbursementRequest.md)
 - [ReimbursementStatus](docs/ReimbursementStatus.md)
 - [ReportAccountBalance](docs/ReportAccountBalance.md)
 - [ReportAccountEntry](docs/ReportAccountEntry.md)
 - [ReportAccountGroup](docs/ReportAccountGroup.md)
 - [ReportAccountGroupNested](docs/ReportAccountGroupNested.md)
 - [ReportBreakdown](docs/ReportBreakdown.md)
 - [ReportBreakdownBy](docs/ReportBreakdownBy.md)
 - [ReportPeriod](docs/ReportPeriod.md)
 - [ReportSection](docs/ReportSection.md)
 - [ReportSummaryLine](docs/ReportSummaryLine.md)
 - [ReportTotals](docs/ReportTotals.md)
 - [ReportingJournalEntry](docs/ReportingJournalEntry.md)
 - [ReportingJournalEntryItem](docs/ReportingJournalEntryItem.md)
 - [Revenue](docs/Revenue.md)
 - [RevenuePattern](docs/RevenuePattern.md)
 - [RevenueRecognitionOnlyContractAmendingItemRequest](docs/RevenueRecognitionOnlyContractAmendingItemRequest.md)
 - [RevenueRecognitionOnlyContractItemRequest](docs/RevenueRecognitionOnlyContractItemRequest.md)
 - [RevenueRecognitionOnlyContractNewItemInAmendmentRequest](docs/RevenueRecognitionOnlyContractNewItemInAmendmentRequest.md)
 - [RevenueRecognitionOnlyContractTerminatedItemRequest](docs/RevenueRecognitionOnlyContractTerminatedItemRequest.md)
 - [RevenueWaterfall](docs/RevenueWaterfall.md)
 - [RoundedMonetaryAmount](docs/RoundedMonetaryAmount.md)
 - [SemiAnnualInvoicing](docs/SemiAnnualInvoicing.md)
 - [SetFieldValueDeactivatedRequest](docs/SetFieldValueDeactivatedRequest.md)
 - [SetupUpAutoPaymentRequest](docs/SetupUpAutoPaymentRequest.md)
 - [Status](docs/Status.md)
 - [Subsidiary](docs/Subsidiary.md)
 - [TaxRate](docs/TaxRate.md)
 - [TaxRateResource](docs/TaxRateResource.md)
 - [TaxRateWithOptionalAmount](docs/TaxRateWithOptionalAmount.md)
 - [Tier](docs/Tier.md)
 - [TieredBilling](docs/TieredBilling.md)
 - [TrialBalanceReport](docs/TrialBalanceReport.md)
 - [UpdateBankTransactionRequest](docs/UpdateBankTransactionRequest.md)
 - [UpdateBillRequest](docs/UpdateBillRequest.md)
 - [UpdateContractRequest](docs/UpdateContractRequest.md)
 - [UpdateCreditMemoRequest](docs/UpdateCreditMemoRequest.md)
 - [UpdateFieldRequest](docs/UpdateFieldRequest.md)
 - [UpdateFieldValueRequest](docs/UpdateFieldValueRequest.md)
 - [UpdateFullContractRequest](docs/UpdateFullContractRequest.md)
 - [UpdateFullInvoiceRequest](docs/UpdateFullInvoiceRequest.md)
 - [UpdateInvoiceRequest](docs/UpdateInvoiceRequest.md)
 - [UpdateInvoiceSentStatusRequest](docs/UpdateInvoiceSentStatusRequest.md)
 - [UpdateItemTaxesRequest](docs/UpdateItemTaxesRequest.md)
 - [UpdateJournalEntryRequest](docs/UpdateJournalEntryRequest.md)
 - [UpdateRevenueRecognitionOnlyContractRequest](docs/UpdateRevenueRecognitionOnlyContractRequest.md)
 - [UpdateRevenueRecognitionOnlyInvoiceItemRequest](docs/UpdateRevenueRecognitionOnlyInvoiceItemRequest.md)
 - [UpdateRevenueRecognitionOnlyInvoiceRequest](docs/UpdateRevenueRecognitionOnlyInvoiceRequest.md)
 - [UpdateTaxesRequest](docs/UpdateTaxesRequest.md)
 - [UpdateVendorCreditRequest](docs/UpdateVendorCreditRequest.md)
 - [Usage](docs/Usage.md)
 - [UsageCommitment](docs/UsageCommitment.md)
 - [UsageConfiguration](docs/UsageConfiguration.md)
 - [UsageInvoiceCycle](docs/UsageInvoiceCycle.md)
 - [UsageInvoiceDate](docs/UsageInvoiceDate.md)
 - [UsageInvoicing](docs/UsageInvoicing.md)
 - [UsageInvoicingFrequency](docs/UsageInvoicingFrequency.md)
 - [UsagePrice](docs/UsagePrice.md)
 - [UsageRecords](docs/UsageRecords.md)
 - [VendorCredit](docs/VendorCredit.md)
 - [VendorCreditApplication](docs/VendorCreditApplication.md)
 - [VendorCreditApplicationRequest](docs/VendorCreditApplicationRequest.md)
 - [VendorCreditLineItem](docs/VendorCreditLineItem.md)
 - [VendorCreditLineItemRequest](docs/VendorCreditLineItemRequest.md)
 - [VendorCreditStatus](docs/VendorCreditStatus.md)
 - [VendorRequest](docs/VendorRequest.md)
 - [VendorResponse](docs/VendorResponse.md)
 - [WebhookContract](docs/WebhookContract.md)
 - [WebhookContractItem](docs/WebhookContractItem.md)
 - [YearlyInvoicing](docs/YearlyInvoicing.md)


## Documentation For Authorization


Authentication schemes defined for the API:
### bearerAuth

- **Type**: HTTP Bearer token authentication

Example

```go
auth := context.WithValue(context.Background(), openapi.ContextAccessToken, "BEARER_TOKEN_STRING")
r, err := client.Service.Operation(auth, args)
```


## Documentation for Utility Methods

Due to the fact that model structure members are all pointers, this package contains
a number of utility functions to easily obtain pointers to values of basic types.
Each of these functions takes a value of the given basic type and returns a pointer to it:

* `PtrBool`
* `PtrInt`
* `PtrInt32`
* `PtrInt64`
* `PtrFloat`
* `PtrFloat32`
* `PtrFloat64`
* `PtrString`
* `PtrTime`

## Author

Mateo ([@mateomaple](https://github.com/mateomaple))

