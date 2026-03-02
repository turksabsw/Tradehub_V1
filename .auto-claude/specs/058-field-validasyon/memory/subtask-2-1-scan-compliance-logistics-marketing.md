# Subtask 2-1: Field Categorization Scan Results
## Apps: tradehub_compliance (23 DocTypes), tradehub_logistics (7 DocTypes), tradehub_marketing (9 DocTypes)

Legend:
- **Category (a)** = SYSTEM-GENERATED/LOCKED: auto-IDs, timestamps, computed values, naming_series, read_only+fetch_from, audit fields
- **Category (b)** = ADMIN-EDITABLE: moderation decisions, status corrections, tenant assignments, system config, compliance decisions
- **Category (c)** = USER-EDITABLE: content fields, selections, ratings, attachments, link selections

Patterns noted: `RO` = read_only:1, `SOO` = set_only_once:1, `H` = hidden:1, `FF:x` = fetch_from:x, `R` = reqd:1, `U` = unique:1

---

## APP: tradehub_compliance (23 DocTypes)

---

### 1. Certificate
**Autoname:** CERT-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | certificate_type | Link | (c) | R | User selects certificate type |
| 2 | type_name | Data | (a) | RO, FF:certificate_type.type_name | Auto-filled |
| 3 | certificate_category | Data | (a) | RO, FF:certificate_type.certificate_category | Auto-filled |
| 4 | status | Select | (b) | R | Admin manages certificate lifecycle |
| 5 | applicable_to | Data | (a) | RO, FF:certificate_type.applicable_to | Auto-filled |
| 6 | sku_product | Link | (c) | mandatory_depends_on | User links product |
| 7 | product_name | Data | (a) | RO, FF:sku_product.product_name | Auto-filled |
| 8 | product_sku_code | Data | (a) | RO, FF:sku_product.sku_code | Auto-filled |
| 9 | seller | Link | (c) | mandatory_depends_on | User links seller |
| 10 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 11 | tenant | Link | (a) | RO | Auto-filled from product/seller |
| 12 | tenant_name | Data | (a) | RO | Auto-filled |
| 13 | certificate_number | Data | (c) | | User enters cert number |
| 14 | issuing_authority | Data | (c) | | User enters authority |
| 15 | issuing_body | Data | (c) | | User enters body |
| 16 | certificate_scope | Small Text | (c) | | User enters scope |
| 17 | issue_date | Date | (c) | R | User enters date |
| 18 | expiry_date | Date | (c) | | User enters date |
| 19 | days_until_expiry | Int | (a) | RO | System-calculated |
| 20 | expiry_status | Select | (a) | RO | System-calculated |
| 21 | requires_renewal | Check | (a) | RO, FF:certificate_type.requires_renewal | Auto-filled |
| 22 | default_validity_months | Int | (a) | RO, FF:certificate_type.default_validity_months | Auto-filled |
| 23 | renewal_reminder_days | Int | (a) | RO, FF:certificate_type.renewal_reminder_days | Auto-filled |
| 24 | renewal_reminder_sent | Check | (a) | RO | System flag |
| 25 | verification_status | Select | (b) | | Admin verifies cert |
| 26 | verification_date | Date | (a) | RO | System timestamp |
| 27 | verified_by | Link | (a) | RO | System captures user |
| 28 | verified_by_name | Data | (a) | RO, FF:verified_by.full_name | Auto-filled |
| 29 | verification_notes | Small Text | (b) | | Admin writes notes |
| 30 | certificate_document | Attach | (c) | | User uploads document |
| 31 | document_filename | Data | (a) | RO | System-populated |
| 32 | verification_url | Data | (c) | | User enters URL |
| 33 | additional_documents | Text | (c) | | User adds documents |
| 34 | previous_certificate | Link | (c) | | User links previous cert |
| 35 | previous_certificate_number | Data | (a) | RO, FF:previous_certificate.certificate_number | Auto-filled |
| 36 | renewed_from | Link | (a) | RO | System link |
| 37 | renewed_to | Link | (a) | RO | System link |
| 38 | description | Text Editor | (c) | | User enters description |
| 39 | internal_notes | Text | (b) | | Admin internal notes |

---

### 2. Certificate Type
**Autoname:** field:type_code

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | type_name | Data | (b) | R | Admin defines type name |
| 2 | type_code | Data | (b) | R, U | Admin defines unique code |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | is_mandatory | Check | (b) | | Admin toggle |
| 5 | certificate_category | Select | (b) | R | Admin selects category |
| 6 | applicable_to | Select | (b) | R | Admin selects scope |
| 7 | standards_body | Data | (b) | | Admin enters |
| 8 | issuing_authority | Data | (b) | | Admin enters |
| 9 | icon | Attach Image | (b) | | Admin uploads icon |
| 10 | description | Text Editor | (b) | | Admin writes description |
| 11 | requirements | Text Editor | (b) | | Admin writes requirements |
| 12 | default_validity_months | Int | (b) | | Admin config |
| 13 | renewal_reminder_days | Int | (b) | | Admin config |
| 14 | requires_physical_audit | Check | (b) | | Admin toggle |
| 15 | requires_renewal | Check | (b) | | Admin toggle |
| 16 | tenant | Link | (b) | | Admin assigns tenant |
| 17 | tenant_name | Data | (a) | RO, FF:tenant.tenant_name | Auto-filled |
| 18 | is_global | Check | (b) | | Admin toggle |
| 19 | website | Data | (b) | | Admin enters URL |
| 20 | reference_standard | Data | (b) | | Admin enters |
| 21 | verification_url | Data | (b) | | Admin enters URL |
| 22 | documentation_url | Data | (b) | | Admin enters URL |
| 23 | display_order | Int | (b) | | Admin config |
| 24 | show_in_filters | Check | (b) | | Admin toggle |
| 25 | featured | Check | (b) | | Admin toggle |
| 26 | certificate_count | Int | (a) | RO | System-computed count |

---

### 3. Consent Audit Log
**Autoname:** naming_series CONSENT-AUDIT-.YYYY.-.#####
**Special:** System Manager has read-only permission (no create/write). All fields read_only:0 but DocType is system-created audit records.

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | consent_record | Link | (a) | R | System sets on creation |
| 3 | action | Select | (a) | R | System sets action |
| 4 | action_by | Link | (a) | R | System captures user |
| 5 | action_date | Datetime | (a) | R | System captures timestamp |
| 6 | details | Small Text | (a) | | System writes details |
| 7 | ip_address | Data | (a) | | System captures IP |
| 8 | user_agent | Small Text | (a) | | System captures UA |
| 9 | old_status | Data | (a) | | System captures state |
| 10 | new_status | Data | (a) | | System captures state |
| 11 | party_type | Data | (a) | | System caches type |
| 12 | party | Data | (a) | | System caches party |

---

### 4. Consent Channel
**Autoname:** field:channel_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | channel_name | Data | (b) | R, U | Admin defines |
| 2 | channel_code | Data | (b) | R, U | Admin defines |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | display_order | Int | (b) | | Admin config |
| 5 | description | Small Text | (b) | | Admin writes |
| 6 | channel_type | Select | (b) | R | Admin selects |
| 7 | icon | Data | (b) | | Admin enters |
| 8 | color | Color | (b) | | Admin picks |
| 9 | requires_verification | Check | (b) | | Admin toggle |
| 10 | default_retention_years | Int | (b) | | Admin config |
| 11 | auto_expire_days | Int | (b) | | Admin config |
| 12 | allow_bulk_consent | Check | (b) | | Admin toggle |
| 13 | tenant | Link | (b) | | Admin assigns |
| 14 | company | Link | (b) | | Admin assigns |

---

### 5. Consent Method
**Autoname:** field:method_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | method_name | Data | (b) | R, U | Admin defines |
| 2 | method_code | Data | (b) | R, U | Admin defines |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | display_order | Int | (b) | | Admin config |
| 5 | description | Small Text | (b) | | Admin writes |
| 6 | method_type | Select | (b) | R | Admin selects |
| 7 | icon | Data | (b) | | Admin enters |
| 8 | color | Color | (b) | | Admin picks |
| 9 | requires_validation | Check | (b) | | Admin toggle |
| 10 | validation_field | Data | (b) | | Admin config |
| 11 | validation_regex | Data | (b) | | Admin config |
| 12 | validation_error_message | Data | (b) | | Admin config |
| 13 | tenant | Link | (b) | | Admin assigns |
| 14 | company | Link | (b) | | Admin assigns |

---

### 6. Consent Record
**Autoname:** naming_series CONSENT-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | party_type | Link | (c) | R | User selects party type |
| 3 | party | Dynamic Link | (c) | R | User selects party |
| 4 | party_name | Data | (a) | RO | Auto-fetched |
| 5 | status | Select | (b) | R | Admin/system manages lifecycle |
| 6 | consent_topic | Link | (c) | R | User selects topic |
| 7 | consent_method | Link | (c) | | User selects method |
| 8 | consent_channel | Link | (c) | | User selects channel |
| 9 | consent_text | Link | (c) | | User links text |
| 10 | consent_text_version | Int | (a) | RO | System captures version |
| 11 | consent_text_hash | Data | (a) | RO | System computes hash |
| 12 | ip_address | Data | (c) | | Captured at consent |
| 13 | user_agent | Small Text | (c) | | Captured at consent |
| 14 | source_url | Data | (c) | | Captured at consent |
| 15 | granted_at | Datetime | (c) | R | User sets grant time |
| 16 | granted_by | Link | (c) | | User who recorded |
| 17 | expiry_date | Date | (c) | | User sets expiry |
| 18 | retention_until | Date | (a) | RO | System auto-calculated |
| 19 | revoked_at | Datetime | (c) | | Set on revocation |
| 20 | revoked_by | Link | (c) | | User who revoked |
| 21 | revocation_reason | Small Text | (c) | | User enters reason |
| 22 | revocation_ip_address | Data | (c) | | Captured at revocation |
| 23 | is_verified | Check | (b) | | Admin/system verifies |
| 24 | verified_at | Datetime | (a) | RO | System timestamp |
| 25 | verification_method | Select | (b) | | Admin selects method |
| 26 | verification_token | Data | (a) | H | System-generated token |
| 27 | double_opt_in_completed | Check | (a) | RO | System flag |
| 28 | tenant | Link | (b) | | Admin assigns tenant |
| 29 | company | Link | (b) | | Admin assigns company |
| 30 | notes | Small Text | (b) | | Admin writes notes |

---

### 7. Consent Text
**Autoname:** naming_series CONSENT-TEXT-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | topic | Link | (b) | R | Admin links topic |
| 3 | language | Link | (b) | R | Admin selects language |
| 4 | status | Select | (b) | R | Admin manages lifecycle |
| 5 | version | Int | (a) | RO | System auto-incremented |
| 6 | title | Data | (b) | R | Admin writes title |
| 7 | content | Text Editor | (b) | R | Admin writes consent text |
| 8 | summary | Small Text | (b) | | Admin writes summary |
| 9 | content_hash | Data | (a) | RO | System-computed hash |
| 10 | previous_version | Link | (a) | RO | System link to previous |
| 11 | legal_basis | Select | (b) | R | Admin selects basis |
| 12 | purpose | Small Text | (b) | | Admin describes purpose |
| 13 | data_categories | Small Text | (b) | | Admin lists categories |
| 14 | retention_period | Int | (b) | | Admin sets retention |
| 15 | retention_unit | Select | (b) | | Admin selects unit |
| 16 | created_by | Link | (a) | RO | System captures user |
| 17 | approved_by | Link | (b) | | Admin records approver |
| 18 | approved_at | Datetime | (a) | RO | System timestamp |
| 19 | superseded_by | Link | (a) | RO | System sets successor |
| 20 | tenant | Link | (b) | | Admin assigns |
| 21 | company | Link | (b) | | Admin assigns |

---

### 8. Consent Topic
**Autoname:** field:topic_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | topic_name | Data | (b) | R, U | Admin defines |
| 2 | topic_code | Data | (b) | R, U | Admin defines |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | display_order | Int | (b) | | Admin config |
| 5 | description | Small Text | (b) | | Admin writes |
| 6 | category | Select | (b) | R | Admin selects |
| 7 | is_mandatory | Check | (b) | | Admin toggle |
| 8 | legal_basis | Select | (b) | R | Admin selects |
| 9 | data_purpose | Small Text | (b) | | Admin describes |
| 10 | icon | Data | (b) | | Admin enters |
| 11 | color | Color | (b) | | Admin picks |
| 12 | retention_years | Int | (b) | | Admin config |
| 13 | requires_double_opt_in | Check | (b) | | Admin toggle |
| 14 | auto_grant_on_registration | Check | (b) | | Admin toggle |
| 15 | tenant | Link | (b) | | Admin assigns |
| 16 | company | Link | (b) | | Admin assigns |

---

### 9. Contract Instance
**Autoname:** naming_series CONTRACT-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | contract_template | Link | (b) | R | Admin/system selects template |
| 3 | status | Select | (b) | R | Admin manages lifecycle |
| 4 | party_type | Link | (b) | R | Admin sets party type |
| 5 | party | Dynamic Link | (b) | R | Admin sets party |
| 6 | party_name | Data | (a) | RO | Auto-fetched |
| 7 | template_version_snapshot | Int | (a) | RO | System captures version |
| 8 | template_content_snapshot | Text Editor | (a) | RO | System captures content |
| 9 | content_hash_snapshot | Data | (a) | RO | System computes hash |
| 10 | created_at | Datetime | (a) | RO | System timestamp |
| 11 | sent_at | Datetime | (a) | RO | System timestamp |
| 12 | esign_transaction | Link | (a) | RO | System link |
| 13 | signed_at | Datetime | (a) | RO | System timestamp |
| 14 | signed_by | Link | (a) | RO | System captures user |
| 15 | rejected_at | Datetime | (a) | RO | System timestamp |
| 16 | rejected_by | Link | (a) | RO | System captures user |
| 17 | rejection_reason | Small Text | (c) | | User enters reason |
| 18 | tenant | Link | (b) | | Admin assigns |
| 19 | company | Link | (b) | | Admin assigns |
| 20 | notes | Small Text | (b) | | Admin notes |

---

### 10. Contract Revision
**Autoname:** naming_series
**Special:** System Manager has read-only permission (no create/write). System-created audit records.

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | contract_template | Link | (a) | R | System links template |
| 3 | version | Int | (a) | R | System version number |
| 4 | action | Select | (a) | R | System records action |
| 5 | changed_by | Link | (a) | | System captures user |
| 6 | changed_at | Datetime | (a) | | System captures timestamp |
| 7 | content_before | Text Editor | (a) | | System captures old content |
| 8 | content_after | Text Editor | (a) | | System captures new content |
| 9 | content_hash_before | Data | (a) | | System captures old hash |
| 10 | content_hash_after | Data | (a) | | System captures new hash |
| 11 | change_summary | Small Text | (a) | | System/admin summary |
| 12 | tenant | Link | (a) | | System captures tenant |

---

### 11. Contract Rule
**Autoname:** naming_series CONTRULE-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | rule_name | Data | (b) | R | Admin defines name |
| 3 | contract_template | Link | (b) | R | Admin selects template |
| 4 | enabled | Check | (b) | | Admin toggle |
| 5 | trigger_on | Select | (b) | R | Admin selects trigger |
| 6 | trigger_doctype | Link | (b) | | Admin selects doctype |
| 7 | priority | Int | (b) | | Admin config |
| 8 | description | Small Text | (b) | | Admin writes |
| 9 | conditions | Table | (b) | | Admin configures conditions |
| 10 | auto_send | Check | (b) | | Admin toggle |
| 11 | require_signature | Check | (b) | | Admin toggle |
| 12 | expiry_days | Int | (b) | | Admin config |
| 13 | last_triggered_at | Datetime | (a) | RO | System timestamp |
| 14 | trigger_count | Int | (a) | RO | System counter |
| 15 | acceptance_count | Int | (a) | RO | System counter |
| 16 | rejection_count | Int | (a) | RO | System counter |
| 17 | tenant | Link | (b) | | Admin assigns |

---

### 12. Contract Template
**Autoname:** naming_series CONTRACT-TPL-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | template_name | Data | (b) | R | Admin defines name |
| 3 | template_code | Data | (b) | R, U | Admin defines code |
| 4 | status | Select | (b) | R | Admin manages lifecycle |
| 5 | contract_type | Select | (b) | R | Admin selects type |
| 6 | version | Int | (a) | RO | System auto-incremented |
| 7 | content | Text Editor | (b) | R | Admin writes template |
| 8 | summary | Small Text | (b) | | Admin writes summary |
| 9 | content_hash | Data | (a) | RO | System-computed hash |
| 10 | validity_days | Int | (b) | | Admin config |
| 11 | requires_signature | Check | (b) | | Admin toggle |
| 12 | published_at | Datetime | (a) | RO | System timestamp |
| 13 | published_by | Link | (a) | RO | System captures user |
| 14 | tenant | Link | (b) | | Admin assigns |
| 15 | company | Link | (b) | | Admin assigns |

---

### 13. ESign Provider
**Autoname:** field:provider_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | provider_name | Data | (b) | R, U | Admin defines name |
| 2 | provider_code | Data | (b) | R, U | Admin defines code |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | provider_type | Select | (b) | R | Admin selects type |
| 5 | api_endpoint | Data | (b) | | Admin config |
| 6 | api_key | Password | (b) | | Admin config (sensitive) |
| 7 | api_secret | Password | (b) | | Admin config (sensitive) |
| 8 | callback_url | Data | (b) | | Admin config |
| 9 | sandbox_mode | Check | (b) | | Admin toggle |
| 10 | sandbox_endpoint | Data | (b) | | Admin config |
| 11 | description | Small Text | (b) | | Admin writes |
| 12 | tenant | Link | (b) | | Admin assigns |

---

### 14. ESign Transaction
**Autoname:** naming_series ESIGN-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | provider | Link | (a) | R | System sets provider |
| 3 | contract_instance | Link | (a) | R | System links contract |
| 4 | status | Select | (b) | R | Admin can override status |
| 5 | external_id | Data | (a) | RO | System from provider API |
| 6 | signer_name | Data | (a) | | System populates |
| 7 | signer_email | Data | (a) | | System populates |
| 8 | signer_phone | Data | (a) | | System populates |
| 9 | signer_tckn | Data | (a) | | System populates |
| 10 | document_hash | Data | (a) | RO | System computes hash |
| 11 | signing_url | Data | (a) | RO | System from provider |
| 12 | signed_pdf | Attach | (a) | | System from provider |
| 13 | signed_at | Datetime | (a) | RO | System timestamp |
| 14 | initiated_at | Datetime | (a) | RO | System timestamp |
| 15 | expires_at | Datetime | (a) | RO | System timestamp |
| 16 | completed_at | Datetime | (a) | RO | System timestamp |
| 17 | error_message | Small Text | (a) | RO | System from provider |
| 18 | error_code | Data | (a) | RO | System from provider |

---

### 15. Marketplace Consent Record
**Autoname:** CONSENT-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | user | Link | (c) | R | User account link |
| 2 | user_full_name | Data | (a) | RO, FF:user.full_name | Auto-filled |
| 3 | consent_type | Select | (c) | R | User selects type |
| 4 | status | Select | (b) | R | Admin manages lifecycle |
| 5 | consent_text | Link | (c) | | User links text |
| 6 | consent_version | Data | (c) | | Version at consent |
| 7 | ip_address | Data | (c) | | Captured at consent |
| 8 | user_agent | Small Text | (c) | | Captured at consent |
| 9 | granted_at | Datetime | (c) | R | Grant timestamp |
| 10 | expiry_date | Date | (c) | | User sets expiry |
| 11 | renewal_reminder_sent | Check | (a) | RO | System flag |
| 12 | revoked_at | Datetime | (c) | | Revocation timestamp |
| 13 | revoked_by | Link | (c) | | Who revoked |
| 14 | revocation_reason | Small Text | (c) | | User enters reason |
| 15 | is_verified | Check | (b) | | Admin/system verifies |
| 16 | verified_at | Datetime | (a) | RO | System timestamp |
| 17 | verified_by | Link | (a) | RO | System captures user |
| 18 | double_opt_in_completed | Check | (a) | RO | System flag |
| 19 | tenant | Link | (b) | | Admin assigns |
| 20 | created_by | Link | (a) | RO | System captures |
| 21 | modified_by | Link | (a) | RO | System captures |
| 22 | amended_from | Link | (a) | RO | System link |

---

### 16. Marketplace Contract Instance
**Autoname:** naming_series CONTRACT-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | contract_template | Link | (b) | R | Admin selects template |
| 3 | template_name | Data | (a) | RO, FF:contract_template.template_name | Auto-filled |
| 4 | status | Select | (b) | R | Admin manages lifecycle |
| 5 | contract_type | Data | (a) | RO, FF:contract_template.contract_type | Auto-filled |
| 6 | buyer | Link | (c) | | User links buyer |
| 7 | buyer_name | Data | (a) | RO, FF:buyer.full_name | Auto-filled |
| 8 | buyer_company | Data | (a) | RO, FF:buyer.company_name | Auto-filled |
| 9 | seller | Link | (c) | | User links seller |
| 10 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 11 | seller_company | Data | (a) | RO, FF:seller.company_name | Auto-filled |
| 12 | rfq | Link | (c) | | User links RFQ |
| 13 | rfq_title | Data | (a) | RO, FF:rfq.title | Auto-filled |
| 14 | related_doctype | Link | (c) | | User selects doctype |
| 15 | related_document | Dynamic Link | (c) | | User links document |
| 16 | rendered_content | Text Editor | (a) | RO | System-rendered |
| 17 | signed_by_buyer | Check | (c) | | Buyer signs |
| 18 | buyer_signature_date | Datetime | (a) | RO | System timestamp |
| 19 | buyer_ip_address | Data | (a) | RO | System captures IP |
| 20 | signed_by_seller | Check | (c) | | Seller signs |
| 21 | seller_signature_date | Datetime | (a) | RO | System timestamp |
| 22 | seller_ip_address | Data | (a) | RO | System captures IP |
| 23 | effective_date | Date | (b) | | Admin sets date |
| 24 | expiry_date | Date | (b) | | Admin sets date |
| 25 | is_expired | Check | (a) | RO | System-calculated |
| 26 | auto_renewed | Check | (a) | RO | System flag |
| 27 | internal_notes | Text | (b) | | Admin notes |

---

### 17. Marketplace Contract Template
**Autoname:** field:template_code

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | template_code | Data | (b) | R, U | Admin defines code |
| 2 | template_name | Data | (b) | R | Admin defines name |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | is_default | Check | (b) | | Admin toggle |
| 5 | description | Small Text | (b) | | Admin writes |
| 6 | content | Text Editor | (b) | R | Admin writes template |
| 7 | contract_type | Select | (b) | R | Admin selects type |
| 8 | validity_days | Int | (b) | | Admin config |
| 9 | requires_signature | Check | (b) | | Admin toggle |
| 10 | auto_expire | Check | (b) | | Admin toggle |
| 11 | tenant | Link | (b) | | Admin assigns |
| 12 | tenant_name | Data | (a) | RO, FF:tenant.tenant_name | Auto-filled |
| 13 | is_global | Check | (b) | | Admin toggle |
| 14 | usage_count | Int | (a) | RO | System counter |
| 15 | last_used_at | Datetime | (a) | RO | System timestamp |

---

### 18. Message
**Autoname:** MSG-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | message_thread | Link | (c) | R | User links to thread |
| 2 | thread_subject | Data | (a) | RO, FF:message_thread.subject | Auto-filled |
| 3 | message_type | Select | (c) | R | User selects type |
| 4 | status | Select | (a) | R | System manages status |
| 5 | sender_type | Select | (c) | R | User selects sender type |
| 6 | sender_user | Link | (c) | | User links sender |
| 7 | sender_name | Data | (a) | RO, FF:sender_user.full_name | Auto-filled |
| 8 | buyer | Link | (c) | | User links buyer |
| 9 | buyer_name | Data | (a) | RO, FF:buyer.buyer_name | Auto-filled |
| 10 | seller | Link | (c) | | User links seller |
| 11 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 12 | content | Text Editor | (c) | R | User writes message |
| 13 | plain_text_content | Long Text | (a) | H | System-generated plain text |
| 14 | has_attachments | Check | (a) | RO | System flag |
| 15 | attachments | JSON | (c) | | User adds attachments |
| 16 | tenant | Link | (a) | RO, FF:message_thread.tenant | Auto-filled |
| 17 | tenant_name | Data | (a) | RO, FF:message_thread.tenant_name | Auto-filled |
| 18 | sent_at | Datetime | (a) | RO | System timestamp |
| 19 | read_at | Datetime | (a) | RO | System timestamp |
| 20 | is_read | Check | (a) | | System updates |
| 21 | is_delivered | Check | (a) | | System updates |
| 22 | delivered_at | Datetime | (a) | RO | System timestamp |
| 23 | delivery_error | Small Text | (a) | RO | System captures error |
| 24 | notification_sent | Check | (a) | | System flag |
| 25 | reply_to | Link | (c) | | User selects reply |
| 26 | reply_to_preview | Small Text | (a) | RO, FF:reply_to.plain_text_content | Auto-filled |
| 27 | is_system_message | Check | (a) | | System flag |
| 28 | is_edited | Check | (a) | | System flag |
| 29 | edited_at | Datetime | (a) | RO | System timestamp |
| 30 | is_flagged | Check | (b) | | Admin flags message |
| 31 | flag_reason | Small Text | (b) | | Admin writes reason |
| 32 | is_deleted | Check | (b) | | Admin soft-deletes |
| 33 | deleted_at | Datetime | (a) | RO | System timestamp |
| 34 | deleted_by | Link | (a) | RO | System captures user |

---

### 19. Message Thread
**Autoname:** THREAD-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | subject | Data | (c) | R | User enters subject |
| 2 | thread_type | Select | (c) | R | User selects type |
| 3 | status | Select | (b) | R | Admin manages status |
| 4 | priority | Select | (b) | | Admin sets priority |
| 5 | buyer | Link | (c) | R | User links buyer |
| 6 | buyer_name | Data | (a) | RO, FF:buyer.buyer_name | Auto-filled |
| 7 | buyer_company | Data | (a) | RO, FF:buyer.company_name | Auto-filled |
| 8 | buyer_email | Data | (a) | RO, FF:buyer.email | Auto-filled |
| 9 | seller | Link | (c) | R | User links seller |
| 10 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 11 | seller_company | Data | (a) | RO, FF:seller.company_name | Auto-filled |
| 12 | seller_email | Data | (a) | RO, FF:seller.email | Auto-filled |
| 13 | tenant | Link | (a) | RO | Auto-filled |
| 14 | tenant_name | Data | (a) | RO | Auto-filled |
| 15 | rfq | Link | (c) | | User links RFQ |
| 16 | rfq_title | Data | (a) | RO, FF:rfq.title | Auto-filled |
| 17 | order | Link | (c) | | User links order |
| 18 | order_status | Data | (a) | RO, FF:order.status | Auto-filled |
| 19 | unread_count | Int | (a) | RO | System counter |
| 20 | message_count | Int | (a) | RO | System counter |
| 21 | last_message_date | Datetime | (a) | RO | System timestamp |
| 22 | last_message_by | Data | (a) | RO | System captures |
| 23 | last_message_preview | Small Text | (a) | RO | System captures |
| 24 | created_date | Datetime | (a) | RO | System timestamp |
| 25 | closed_date | Datetime | (a) | RO | System timestamp |
| 26 | archived_date | Datetime | (a) | RO | System timestamp |

---

### 20. Moderation Case
**Autoname:** MOD-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | case_id | Data | (a) | RO, U | System-generated ID |
| 2 | content_type | Link | (b) | R | Admin sets content type |
| 3 | content_id | Dynamic Link | (b) | R | Admin links content |
| 4 | content_title | Data | (a) | RO | System captures |
| 5 | status | Select | (b) | R | Admin manages case status |
| 6 | priority | Select | (b) | R | Admin sets priority |
| 7 | category | Select | (b) | R | Admin categorizes |
| 8 | subcategory | Select | (b) | | Admin sub-categorizes |
| 9 | reporter_type | Select | (c) | | Reporter type |
| 10 | reporter | Link | (c) | | Reporter link |
| 11 | report_reason | Select | (c) | | Reporter's reason |
| 12 | report_description | Small Text | (c) | | Reporter's description |
| 13 | created_by_user | Link | (a) | RO | System captures |
| 14 | creation_date | Datetime | (a) | RO | System timestamp |
| 15 | content_created_at | Datetime | (a) | RO | System captures |
| 16 | assigned_to | Link | (b) | | Admin assigns moderator |
| 17 | assigned_at | Datetime | (a) | RO | System timestamp |
| 18 | review_started_at | Datetime | (a) | RO | System timestamp |
| 19 | review_completed_at | Datetime | (a) | RO | System timestamp |
| 20 | reviewed_by | Link | (a) | RO | System captures |
| 21 | review_time_seconds | Int | (a) | RO | System calculated |
| 22 | decision | Select | (b) | | Admin decision |
| 23 | decision_reason | Small Text | (b) | | Admin reason |
| 24 | action_taken | Select | (b) | | Admin action |
| 25 | action_details | Small Text | (b) | | Admin details |
| 26 | content_removed | Check | (b) | | Admin action |
| 27 | user_warned | Check | (b) | | Admin action |
| 28 | user_suspended | Check | (b) | | Admin action |
| 29 | appeal_status | Select | (b) | | Admin manages appeal |
| 30 | appeal_reason | Small Text | (c) | | User submits appeal |
| 31 | appeal_submitted_at | Datetime | (a) | RO | System timestamp |
| 32 | appeal_decision | Select | (b) | | Admin appeal decision |
| 33 | appeal_decision_reason | Small Text | (b) | | Admin writes |
| 34 | appeal_decided_by | Link | (a) | RO | System captures |
| 35 | appeal_decided_at | Datetime | (a) | RO | System timestamp |
| 36 | escalated_to | Link | (b) | | Admin escalates |
| 37 | escalated_at | Datetime | (a) | RO | System timestamp |
| 38 | escalated_by | Link | (a) | RO | System captures |
| 39 | escalation_reason | Small Text | (b) | | Admin reason |
| 40 | owner_notified | Check | (a) | RO | System flag |
| 41 | owner_notified_at | Datetime | (a) | RO | System timestamp |
| 42 | reporter_notified | Check | (a) | RO | System flag |
| 43 | reporter_notified_at | Datetime | (a) | RO | System timestamp |
| 44 | decision_notification_sent | Check | (a) | RO | System flag |
| 45 | queue_position | Int | (a) | RO | System calculated |
| 46 | wait_time_hours | Float | (a) | RO | System calculated |
| 47 | resolution_time_hours | Float | (a) | RO | System calculated |
| 48 | sla_status | Select | (a) | RO | System calculated |
| 49 | detection_flags | JSON | (a) | | System detection data |
| 50 | moderation_history | JSON | (a) | RO | System history |
| 51 | tenant | Link | (b) | | Admin assigns |

---

### 21. Review
**Autoname:** naming_series REV-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | review_id | Data | (a) | RO, U | System-generated ID |
| 3 | reviewer | Link | (c) | R | User links reviewer |
| 4 | reviewer_name | Data | (a) | RO, FF:reviewer.full_name | Auto-filled |
| 5 | listing | Link | (c) | R | User links listing |
| 6 | listing_title | Data | (a) | RO, FF:listing.listing_title | Auto-filled |
| 7 | seller | Link | (a) | | System populated |
| 8 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 9 | status | Select | (b) | R | Admin manages lifecycle |
| 10 | category | Select | (a) | RO | System-determined |
| 11 | overall_rating | Rating | (c) | R | User rates |
| 12 | title | Data | (c) | | User writes title |
| 13 | review_text | Text Editor | (c) | R | User writes review |
| 14 | pros | Small Text | (c) | | User writes pros |
| 15 | cons | Small Text | (c) | | User writes cons |
| 16 | is_verified_purchase | Check | (a) | RO | System verifies |
| 17 | purchase_date | Date | (a) | RO | System captures |
| 18 | verification_date | Date | (a) | RO | System captures |
| 19 | images | JSON | (c) | | User uploads images |
| 20 | helpful_count | Int | (a) | RO | System counter |
| 21 | unhelpful_count | Int | (a) | RO | System counter |
| 22 | helpfulness_score | Float | (a) | RO | System calculated |
| 23 | report_count | Int | (a) | RO | System counter |
| 24 | has_seller_response | Check | (a) | RO | System flag |
| 25 | seller_response | Text Editor | (c) | | Seller writes response |
| 26 | seller_response_by | Link | (a) | RO | System captures |
| 27 | seller_response_at | Datetime | (a) | RO | System timestamp |
| 28 | response_helpful_count | Int | (a) | RO | System counter |
| 29 | moderation_status | Select | (b) | | Admin moderates |
| 30 | moderation_notes | Small Text | (b) | | Admin writes notes |
| 31 | moderated_by | Link | (a) | RO | System captures |
| 32 | moderated_at | Datetime | (a) | RO | System timestamp |
| 33 | flags | JSON | (b) | | Admin flags |
| 34 | submitted_at | Datetime | (a) | RO | System timestamp |
| 35 | published_at | Datetime | (a) | RO | System timestamp |
| 36 | last_edited_at | Datetime | (a) | RO | System timestamp |
| 37 | edit_count | Int | (a) | RO | System counter |
| 38 | ip_address | Data | (a) | RO | System captures |
| 39 | user_agent | Data | (a) | RO | System captures |
| 40 | tenant | Link | (b) | | Admin assigns |

---

### 22. Risk Score
**Autoname:** RISK-.######

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | entity_type | Select | (b) | R | Admin sets entity type |
| 2 | seller | Link | (b) | | Admin links seller |
| 3 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 4 | buyer | Link | (b) | | Admin links buyer |
| 5 | buyer_name | Data | (a) | RO, FF:buyer.full_name | Auto-filled |
| 6 | tenant | Link | (a) | RO | Auto-filled |
| 7 | tenant_name | Data | (a) | RO, FF:tenant.tenant_name | Auto-filled |
| 8 | overall_score | Float | (b) | R | Admin/system sets score |
| 9 | risk_level | Select | (b) | R | Admin/system sets level |
| 10 | previous_score | Float | (a) | RO | System captures |
| 11 | score_change | Float | (a) | RO | System calculated |
| 12 | score_trend | Select | (a) | RO | System calculated |
| 13 | total_weight | Float | (a) | RO | System calculated |
| 14 | weighted_average | Float | (a) | RO | System calculated |
| 15 | positive_factors_count | Int | (a) | RO | System calculated |
| 16 | negative_factors_count | Int | (a) | RO | System calculated |
| 17 | critical_factors_count | Int | (a) | RO | System calculated |
| 18 | risk_factors | JSON | (b) | | Admin/system risk data |
| 19 | confidence_level | Select | (a) | RO | System calculated |
| 20 | auto_decision | Select | (a) | RO | System decision |
| 21 | manual_override | Check | (b) | | Admin override |
| 22 | override_reason | Small Text | (b) | | Admin reason |
| 23 | override_by | Link | (a) | RO | System captures |
| 24 | override_at | Datetime | (a) | RO | System timestamp |
| 25 | last_calculated_at | Datetime | (a) | RO | System timestamp |
| 26 | calculation_history | JSON | (a) | RO | System history |
| 27 | has_alerts | Check | (a) | RO | System flag |
| 28 | alert_count | Int | (a) | RO | System counter |
| 29 | last_alert_at | Datetime | (a) | RO | System timestamp |
| 30 | alert_summary | Small Text | (a) | RO | System summary |
| 31 | created_at | Datetime | (a) | RO | System timestamp |
| 32 | created_by | Link | (a) | RO | System captures |
| 33 | modified_at | Datetime | (a) | RO | System timestamp |
| 34 | modified_by_user | Link | (a) | RO | System captures |

---

### 23. Sample Request
**Autoname:** SMP-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | sku_product | Link | (c) | R | User links product |
| 2 | product_name | Data | (a) | RO, FF:sku_product.product_name | Auto-filled |
| 3 | product_sku_code | Data | (a) | RO, FF:sku_product.sku_code | Auto-filled |
| 4 | product_status | Data | (a) | RO, FF:sku_product.status | Auto-filled |
| 5 | variant | Link | (c) | | User links variant |
| 6 | variant_name | Data | (a) | RO, FF:variant.variant_name | Auto-filled |
| 7 | seller | Link | (a) | RO, FF:sku_product.seller | Auto-filled |
| 8 | seller_name | Data | (a) | RO, FF:sku_product.seller_name | Auto-filled |
| 9 | tenant | Link | (a) | RO, FF:sku_product.tenant | Auto-filled |
| 10 | tenant_name | Data | (a) | RO, FF:sku_product.tenant_name | Auto-filled |
| 11 | status | Select | (b) | R | Admin manages request |
| 12 | buyer | Link | (c) | R | User links buyer |
| 13 | buyer_name | Data | (a) | RO, FF:buyer.full_name | Auto-filled |
| 14 | buyer_company | Data | (a) | RO, FF:buyer.company_name | Auto-filled |
| 15 | buyer_email | Data | (a) | RO, FF:buyer.email | Auto-filled |
| 16 | buyer_phone | Data | (a) | RO, FF:buyer.phone | Auto-filled |
| 17 | quantity | Int | (c) | R | User enters quantity |
| 18 | sample_type | Select | (c) | R | User selects type |
| 19 | purpose | Small Text | (c) | | User describes purpose |
| 20 | shipping_address | Small Text | (c) | | User enters address |
| 21 | special_requirements | Small Text | (c) | | User enters requirements |
| 22 | total_cost | Currency | (a) | RO | System calculated |
| 23 | approved_date | Date | (a) | RO | System timestamp |
| 24 | approval_notes | Small Text | (b) | | Admin writes notes |
| 25 | rejection_reason | Small Text | (b) | | Admin writes reason |
| 26 | tracking_number | Data | (b) | | Admin enters tracking |
| 27 | shipped_date | Date | (b) | | Admin enters date |
| 28 | delivery_date | Date | (b) | | Admin enters date |
| 29 | credited_amount | Currency | (a) | RO | System calculated |
| 30 | credited_order | Link | (a) | RO | System link |
| 31 | feedback | Small Text | (c) | | User writes feedback |
| 32 | feedback_rating | Rating | (c) | | User rates |

---

## APP: tradehub_logistics (7 DocTypes)

---

### 24. Carrier
**Autoname:** field:carrier_code

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | carrier_name | Data | (b) | R | Admin defines carrier |
| 2 | carrier_code | Data | (b) | R, U | Admin defines code |
| 3 | enabled | Check | (b) | | Admin toggle |
| 4 | is_default | Check | (b) | | Admin toggle |
| 5 | carrier_type | Select | (b) | R | Admin selects type |
| 6 | service_methods | Small Text | (b) | | Admin lists methods |
| 7 | supports_tracking | Check | (b) | | Admin toggle |
| 8 | supports_cod | Check | (b) | | Admin toggle |
| 9 | supports_insurance | Check | (b) | | Admin toggle |
| 10 | contact_person | Data | (b) | | Admin enters |
| 11 | email | Data | (b) | | Admin enters |
| 12 | phone | Data | (b) | | Admin enters |
| 13 | website | Data | (b) | | Admin enters |
| 14 | address | Small Text | (b) | | Admin enters |
| 15 | city | Data | (b) | | Admin enters |
| 16 | country | Link | (b) | | Admin selects |
| 17 | postal_code | Data | (b) | | Admin enters |
| 18 | tenant | Link | (b) | | Admin assigns |
| 19 | tenant_name | Data | (a) | RO, FF:tenant.tenant_name | Auto-filled |
| 20 | is_global | Check | (b) | | Admin toggle |
| 21 | domestic_only | Check | (b) | | Admin toggle |
| 22 | service_countries | Small Text | (b) | | Admin config |
| 23 | excluded_countries | Small Text | (b) | | Admin config |
| 24 | service_regions | Small Text | (b) | | Admin config |
| 25 | has_api_integration | Check | (b) | | Admin toggle |
| 26 | api_provider | Select | (b) | | Admin selects |
| 27 | api_version | Data | (b) | | Admin enters |
| 28 | api_endpoint | Data | (b) | | Admin enters |
| 29 | api_key | Password | (b) | | Admin config (sensitive) |
| 30 | api_secret | Password | (b) | | Admin config (sensitive) |
| 31 | api_account_number | Data | (b) | | Admin enters |
| 32 | api_environment | Select | (b) | | Admin selects |
| 33 | api_timeout | Int | (b) | | Admin config |
| 34 | api_last_checked | Datetime | (a) | RO | System timestamp |
| 35 | api_status | Select | (a) | RO | System status |
| 36 | api_error_message | Small Text | (a) | RO | System error |
| 37 | supports_rate_api | Check | (b) | | Admin toggle |
| 38 | supports_label_api | Check | (b) | | Admin toggle |
| 39 | webhook_enabled | Check | (b) | | Admin toggle |
| 40 | webhook_url | Data | (b) | | Admin enters |
| 41 | webhook_secret | Password | (b) | | Admin config (sensitive) |
| 42 | webhook_events | Small Text | (b) | | Admin config |
| 43 | tracking_url_template | Data | (b) | | Admin config |
| 44 | tracking_api_enabled | Check | (b) | | Admin toggle |
| 45 | tracking_update_frequency | Int | (b) | | Admin config |
| 46 | default_transit_days | Int | (b) | | Admin config |
| 47 | min_weight | Float | (b) | | Admin config |
| 48 | max_weight | Float | (b) | | Admin config |
| 49 | weight_uom | Link | (b) | | Admin selects |
| 50 | dimensional_divisor | Int | (b) | | Admin config |
| 51 | fuel_surcharge_percent | Percent | (b) | | Admin config |
| 52 | base_rate | Currency | (b) | | Admin config |
| 53 | rate_per_kg | Currency | (b) | | Admin config |
| 54 | currency | Link | (b) | | Admin selects |
| 55 | pricing_notes | Small Text | (b) | | Admin writes |
| 56 | logo | Attach Image | (b) | | Admin uploads |
| 57 | description | Text Editor | (b) | | Admin writes |
| 58 | display_order | Int | (b) | | Admin config |
| 59 | show_in_checkout | Check | (b) | | Admin toggle |
| 60 | featured | Check | (b) | | Admin toggle |
| 61 | shipment_count | Int | (a) | RO | System counter |
| 62 | internal_notes | Text | (b) | | Admin notes |

---

### 25. Lead Time
**Autoname:** LT-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | sku_product | Link | (c) | R | Seller links product |
| 2 | product_name | Data | (a) | RO, FF:sku_product.product_name | Auto-filled |
| 3 | product_sku_code | Data | (a) | RO, FF:sku_product.sku_code | Auto-filled |
| 4 | product_status | Data | (a) | RO, FF:sku_product.status | Auto-filled |
| 5 | seller | Link | (a) | RO, FF:sku_product.seller | Auto-filled |
| 6 | seller_name | Data | (a) | RO, FF:sku_product.seller_name | Auto-filled |
| 7 | tenant | Link | (a) | RO, FF:sku_product.tenant | Auto-filled |
| 8 | tenant_name | Data | (a) | RO, FF:sku_product.tenant_name | Auto-filled |
| 9 | lead_time_type | Select | (c) | R | Seller selects type |
| 10 | lead_time_days | Int | (c) | R | Seller enters days |
| 11 | status | Select | (b) | R | Admin/seller manages |
| 12 | is_default | Check | (c) | | Seller toggle |
| 13 | min_order_quantity | Float | (c) | | Seller enters |
| 14 | max_order_quantity | Float | (c) | | Seller enters |
| 15 | production_capacity | Int | (c) | | Seller enters |
| 16 | capacity_period | Select | (c) | | Seller selects |
| 17 | valid_from | Date | (c) | | Seller enters |
| 18 | valid_until | Date | (c) | | Seller enters |
| 19 | priority | Int | (c) | | Seller config |
| 20 | applies_to_region | Data | (c) | | Seller enters |
| 21 | notes | Small Text | (c) | | Seller writes |

---

### 26. Logistics Provider
**Autoname:** field:provider_code

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | provider_name | Data | (b) | R | Admin defines name |
| 2 | provider_code | Data | (b) | R, U | Admin defines code |
| 3 | provider_type | Select | (b) | R | Admin selects type |
| 4 | status | Select | (b) | R | Admin manages status |
| 5 | logo | Attach Image | (b) | | Admin uploads |
| 6 | website | Data | (b) | | Admin enters |
| 7 | description | Small Text | (b) | | Admin writes |
| 8 | contact_person | Data | (b) | | Admin enters |
| 9 | contact_email | Data | (b) | | Admin enters |
| 10 | contact_phone | Data | (b) | | Admin enters |
| 11 | support_email | Data | (b) | | Admin enters |
| 12 | support_phone | Data | (b) | | Admin enters |
| 13 | support_hours | Data | (b) | | Admin enters |
| 14 | api_enabled | Check | (b) | | Admin toggle |
| 15 | api_endpoint | Data | (b) | | Admin config |
| 16 | api_version | Data | (b) | | Admin config |
| 17 | api_key | Password | (b) | | Admin config (sensitive) |
| 18 | api_secret | Password | (b) | | Admin config (sensitive) |
| 19 | api_username | Data | (b) | | Admin config |
| 20 | api_password | Password | (b) | | Admin config (sensitive) |
| 21 | api_timeout | Int | (b) | | Admin config |
| 22 | api_retry_count | Int | (b) | | Admin config |
| 23 | sandbox_mode | Check | (b) | | Admin toggle |
| 24 | sandbox_endpoint | Data | (b) | | Admin config |
| 25 | supports_tracking | Check | (b) | | Admin toggle |
| 26 | tracking_url_template | Data | (b) | | Admin config |
| 27 | tracking_update_frequency | Int | (b) | | Admin config |
| 28 | supports_webhooks | Check | (b) | | Admin toggle |
| 29 | webhook_url | Data | (a) | RO | System-generated |
| 30 | webhook_secret | Password | (b) | | Admin config (sensitive) |
| 31 | service_type | Select | (b) | R | Admin selects |
| 32 | domestic_coverage | Check | (b) | | Admin toggle |
| 33 | international_coverage | Check | (b) | | Admin toggle |
| 34 | served_countries | Small Text | (b) | | Admin config |
| 35 | excluded_regions | Small Text | (b) | | Admin config |
| 36 | supported_shipping_methods | Small Text | (b) | | Admin config |
| 37 | default_shipping_method | Data | (b) | | Admin config |
| 38 | supports_express | Check | (b) | | Admin toggle |
| 39 | supports_same_day | Check | (b) | | Admin toggle |
| 40 | supports_cod | Check | (b) | | Admin toggle |
| 41 | supports_insurance | Check | (b) | | Admin toggle |
| 42 | rate_calculation_method | Select | (b) | | Admin selects |
| 43 | base_rate | Currency | (b) | | Admin config |
| 44 | rate_per_kg | Currency | (b) | | Admin config |
| 45 | fuel_surcharge_percent | Percent | (b) | | Admin config |
| 46 | min_chargeable_weight | Float | (b) | | Admin config |
| 47 | volumetric_divisor | Int | (b) | | Admin config |
| 48 | max_weight_kg | Float | (b) | | Admin config |
| 49 | max_length_cm | Float | (b) | | Admin config |
| 50 | max_width_cm | Float | (b) | | Admin config |
| 51 | max_height_cm | Float | (b) | | Admin config |
| 52 | max_volume_cm3 | Float | (b) | | Admin config |
| 53 | max_declared_value | Currency | (b) | | Admin config |
| 54 | currency | Link | (b) | | Admin selects |
| 55 | label_format | Select | (b) | | Admin selects |
| 56 | label_size | Select | (b) | | Admin selects |
| 57 | supports_pickup | Check | (b) | | Admin toggle |
| 58 | supports_dropoff | Check | (b) | | Admin toggle |
| 59 | supports_return_label | Check | (b) | | Admin toggle |
| 60 | average_delivery_days | Float | (a) | RO | System calculated |
| 61 | on_time_delivery_rate | Percent | (a) | RO | System calculated |
| 62 | damage_rate | Percent | (a) | RO | System calculated |
| 63 | total_shipments | Int | (a) | RO | System counter |
| 64 | total_issues | Int | (a) | RO | System counter |
| 65 | last_used_at | Datetime | (a) | RO | System timestamp |
| 66 | is_default | Check | (b) | | Admin toggle |
| 67 | priority | Int | (b) | | Admin config |
| 68 | notes | Small Text | (b) | | Admin notes |
| 69 | enabled_for_sellers | Check | (b) | | Admin toggle |
| 70 | enabled_for_marketplace | Check | (b) | | Admin toggle |
| 71 | requires_contract | Check | (b) | | Admin toggle |

---

### 27. Marketplace Shipment
**Autoname:** naming_series SHP-.YYYY.-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | shipment_id | Data | (a) | RO, U | System-generated ID |
| 2 | sub_order | Link | (c) | R | Seller links sub order |
| 3 | seller | Link | (c) | | Seller link |
| 4 | status | Select | (b) | R | Admin/system manages status |
| 5 | shipment_type | Select | (c) | | Seller selects type |
| 6 | tenant | Link | (b) | | Admin assigns |
| 7 | carrier | Select | (c) | R | Seller selects carrier |
| 8 | carrier_account | Data | (c) | | Seller enters |
| 9 | service_type | Data | (c) | | Seller enters |
| 10 | tracking_number | Data | (c) | | Seller enters |
| 11 | tracking_url | Data | (c) | | Seller enters |
| 12 | awb_number | Data | (c) | | Seller enters |
| 13 | sender_name | Data | (c) | R | Seller enters |
| 14 | sender_phone | Data | (c) | | Seller enters |
| 15 | origin_address_line1 | Data | (c) | R | Seller enters |
| 16 | origin_address_line2 | Data | (c) | | Seller enters |
| 17 | origin_city | Data | (c) | R | Seller enters |
| 18 | origin_state | Data | (c) | | Seller enters |
| 19 | origin_postal_code | Data | (c) | | Seller enters |
| 20 | origin_country | Link | (c) | R | Seller selects |
| 21 | recipient_name | Data | (c) | R | From order |
| 22 | recipient_phone | Data | (c) | | From order |
| 23 | destination_address_line1 | Data | (c) | R | From order |
| 24 | destination_address_line2 | Data | (c) | | From order |
| 25 | destination_city | Data | (c) | R | From order |
| 26 | destination_state | Data | (c) | | From order |
| 27 | destination_postal_code | Data | (c) | | From order |
| 28 | destination_country | Link | (c) | R | From order |
| 29 | package_count | Int | (c) | | Seller enters |
| 30 | total_weight | Float | (c) | | Seller enters |
| 31 | weight_unit | Select | (c) | | Seller selects |
| 32 | total_length | Float | (c) | | Seller enters |
| 33 | total_width | Float | (c) | | Seller enters |
| 34 | total_height | Float | (c) | | Seller enters |
| 35 | dimension_unit | Select | (c) | | Seller selects |
| 36 | volumetric_weight | Float | (a) | RO | System calculated |
| 37 | description | Small Text | (c) | | Seller enters |
| 38 | declared_value | Currency | (c) | | Seller enters |
| 39 | currency | Link | (c) | | Seller selects |
| 40 | contains_fragile | Check | (c) | | Seller toggle |
| 41 | contains_hazmat | Check | (c) | | Seller toggle |
| 42 | requires_signature | Check | (c) | | Seller toggle |
| 43 | shipping_cost | Currency | (c) | | Seller/system enters |
| 44 | insurance_cost | Currency | (c) | | Seller enters |
| 45 | handling_cost | Currency | (c) | | Seller enters |
| 46 | additional_charges | Currency | (c) | | System charges |
| 47 | total_cost | Currency | (a) | RO | System calculated |
| 48 | cost_currency | Link | (c) | | Seller selects |
| 49 | pickup_date | Date | (c) | | Seller enters |
| 50 | pickup_time_from | Time | (c) | | Seller enters |
| 51 | pickup_time_to | Time | (c) | | Seller enters |
| 52 | expected_delivery_date | Date | (c) | | System/seller enters |
| 53 | actual_delivery_date | Date | (a) | | System captures |
| 54 | delivery_time | Time | (a) | | System captures |
| 55 | delivery_status | Select | (b) | | Admin/system status |
| 56 | delivery_attempts | Int | (a) | | System counter |
| 57 | delivered_to | Data | (a) | | System captures |
| 58 | delivery_signature | Attach Image | (a) | | System captures |
| 59 | proof_of_delivery | Attach Image | (a) | | System captures |
| 60 | delivery_notes | Small Text | (b) | | Admin/carrier notes |
| 61 | created_at | Datetime | (a) | RO | System timestamp |
| 62 | picked_up_at | Datetime | (a) | RO | System timestamp |
| 63 | in_transit_at | Datetime | (a) | RO | System timestamp |
| 64 | out_for_delivery_at | Datetime | (a) | RO | System timestamp |
| 65 | delivered_at | Datetime | (a) | RO | System timestamp |
| 66 | exception_at | Datetime | (a) | RO | System timestamp |
| 67 | is_return | Check | (c) | | Seller/admin flag |
| 68 | return_reason | Select | (c) | | Reason for return |
| 69 | original_shipment | Link | (c) | | Links original |
| 70 | return_status | Select | (b) | | Admin manages |
| 71 | return_tracking_number | Data | (c) | | Seller enters |
| 72 | label_generated | Check | (a) | | System flag |
| 73 | label_url | Data | (a) | | System from API |
| 74 | label_format | Select | (c) | | Seller selects |
| 75 | manifest_id | Data | (a) | | System from API |
| 76 | batch_id | Data | (a) | | System from API |
| 77 | seller_notes | Small Text | (c) | | Seller writes |
| 78 | internal_notes | Small Text | (b) | | Admin writes |
| 79 | carrier_notes | Small Text | (a) | | System/carrier |
| 80 | naming_series | Select | (a) | H | System naming |
| 81 | carrier_response | Code | (a) | RO | System from API |
| 82 | last_sync_at | Datetime | (a) | RO | System timestamp |
| 83 | logistics_provider | Link | (c) | | Seller links |
| 84 | package_length | Float | (c) | | Seller enters |
| 85 | package_width | Float | (c) | | Seller enters |
| 86 | package_height | Float | (c) | | Seller enters |
| 87 | total_volume | Float | (a) | | System calculated |
| 88 | pod_verified | Check | (b) | | Admin verifies |
| 89 | received_by | Data | (a) | | System captures |
| 90 | receiver_signature | Attach Image | (a) | | System captures |
| 91 | signature_captured_at | Datetime | (a) | | System timestamp |

---

### 28. Shipment
**Autoname:** SHIP-.#####

(Largest logistics DocType ~100+ fields. Key categorization follows same patterns)

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | shipment_number | Data | (a) | RO | System-generated |
| 2 | status | Select | (b) | R | Admin manages status |
| 3 | shipment_date | Date | (c) | R | Seller enters |
| 4 | shipment_type | Select | (c) | R | Seller selects |
| 5 | priority | Select | (b) | | Admin sets |
| 6 | order | Link | (c) | R | Seller links order |
| 7 | order_number | Data | (a) | RO, FF:order.order_number | Auto-filled |
| 8 | order_status | Data | (a) | RO, FF:order.status | Auto-filled |
| 9 | order_type | Data | (a) | RO, FF:order.order_type | Auto-filled |
| 10 | order_total | Currency | (a) | RO, FF:order.total_amount | Auto-filled |
| 11 | sub_order | Link | (c) | | Seller links sub order |
| 12 | sub_order_id | Data | (a) | RO, FF:sub_order.sub_order_id | Auto-filled |
| 13 | sub_order_status | Data | (a) | RO, FF:sub_order.status | Auto-filled |
| 14 | sub_order_total | Currency | (a) | RO, FF:sub_order.grand_total | Auto-filled |
| 15 | buyer | Link | (a) | RO, FF:order.buyer | Auto-filled |
| 16 | buyer_name | Data | (a) | RO, FF:order.buyer_name | Auto-filled |
| 17 | buyer_company | Data | (a) | RO, FF:order.buyer_company | Auto-filled |
| 18 | buyer_email | Data | (a) | RO, FF:order.buyer_email | Auto-filled |
| 19 | buyer_phone | Data | (a) | RO, FF:order.buyer_phone | Auto-filled |
| 20 | seller | Link | (a) | RO, FF:order.seller | Auto-filled |
| 21 | seller_name | Data | (a) | RO, FF:order.seller_name | Auto-filled |
| 22 | seller_company | Data | (a) | RO, FF:order.seller_company | Auto-filled |
| 23 | seller_email | Data | (a) | RO, FF:order.seller_email | Auto-filled |
| 24 | seller_phone | Data | (a) | RO, FF:order.seller_phone | Auto-filled |
| 25 | tenant | Link | (a) | RO, FF:order.tenant | Auto-filled |
| 26 | tenant_name | Data | (a) | RO, FF:order.tenant_name | Auto-filled |
| 27 | carrier | Link | (c) | | Seller selects carrier |
| 28 | carrier_name | Data | (a) | RO, FF:carrier.carrier_name | Auto-filled |
| 29 | carrier_account_number | Data | (c) | | Seller enters |
| 30 | shipping_method | Select | (c) | | Seller selects |
| 31 | service_type | Data | (c) | | Seller enters |
| 32 | carrier_reference | Data | (c) | | Seller/system enters |
| 33 | tracking_number | Data | (c) | | Seller enters |
| 34 | tracking_url | Data | (c) | | Seller/system enters |
| 35 | tracking_status | Select | (b) | | Admin/system status |
| 36 | last_tracking_update | Datetime | (a) | RO | System timestamp |
| 37 | tracking_events | Text | (a) | RO | System JSON |
| 38 | label_generated | Check | (a) | RO | System flag |
| 39 | label_url | Data | (a) | RO | System from API |
| 40 | label_data | Attach | (a) | | System from API |
| 41 | carrier_shipment_id | Data | (a) | RO | System from API |
| 42-50 | origin_* | Data/Link | (c) | | Seller enters origin address |
| 51-58 | destination_* | Data/Link | (c) | | Seller enters destination |
| 59 | package_count | Int | (c) | | Seller enters |
| 60 | total_weight | Float | (c) | | Seller enters |
| 61 | weight_uom | Link | (c) | | Seller selects |
| 62 | total_volume | Float | (c) | | Seller enters |
| 63 | volume_uom | Data | (c) | | Seller enters |
| 64 | package_description | Small Text | (c) | | Seller enters |
| 65 | length/width/height | Float | (c) | | Seller enters |
| 66 | dimension_uom | Link | (c) | | Seller selects |
| 67 | dimensional_weight | Float | (a) | RO | System calculated |
| 68 | requires_customs | Check | (c) | | Seller toggle |
| 69 | customs_status | Select | (b) | | Admin manages |
| 70 | customs_value | Currency | (c) | | Seller enters |
| 71 | customs_currency | Link | (c) | | Seller selects |
| 72-75 | customs docs | Data | (c) | | Seller enters |
| 76-78 | customs items | Data/Int/Currency | (c) | | Seller enters |
| 79-80 | customs_duty/tax | Currency | (c) | | Entered/calculated |
| 81 | customs_clearance_date | Date | (a) | RO | System timestamp |
| 82 | is_insured | Check | (c) | | Seller toggle |
| 83 | insurance_value | Currency | (c) | | Seller enters |
| 84 | insurance_provider | Data | (c) | | Seller enters |
| 85 | insurance_policy_number | Data | (c) | | Seller enters |
| 86 | incoterm | Select | (c) | | Seller selects |
| 87 | incoterm_description | Data | (a) | RO | System auto-generated |
| 88 | freight_cost | Currency | (c) | | Seller enters |
| 89 | insurance_cost | Currency | (c) | | Seller enters |
| 90 | total_shipping_cost | Currency | (a) | RO | System calculated |
| 91 | pickup_date | Date | (c) | | Seller enters |
| 92 | pickup_time | Time | (c) | | Seller enters |
| 93 | estimated_delivery_date | Date | (c) | | Seller/system |
| 94 | actual_delivery_date | Date | (a) | RO | System captures |
| 95 | delivery_time | Time | (a) | RO | System captures |
| 96 | in_transit_date | Datetime | (a) | RO | System timestamp |
| 97 | customs_clearance_start | Datetime | (a) | RO | System timestamp |
| 98 | out_for_delivery_date | Datetime | (a) | RO | System timestamp |
| 99 | exception_date | Datetime | (a) | RO | System timestamp |
| 100 | pod_received | Check | (b) | | Admin verifies |
| 101 | pod_signature | Data | (b) | | Admin enters |
| 102 | pod_image | Attach Image | (b) | | Admin uploads |
| 103 | pod_notes | Small Text | (b) | | Admin writes |
| 104 | special_handling | Small Text | (c) | | Seller enters |
| 105 | delivery_instructions | Small Text | (c) | | Seller enters |
| 106 | is_hazardous | Check | (c) | | Seller toggle |
| 107 | hazmat_class | Data | (c) | | Seller enters |
| 108 | linked_delivery_note | Data | (a) | RO | System link |
| 109 | linked_sales_order | Data | (a) | RO | System link |
| 110 | linked_packing_slip | Data | (c) | | Seller enters |
| 111 | linked_bill_of_lading | Data | (c) | | Seller enters |
| 112 | internal_notes | Text | (b) | | Admin notes |
| 113 | carrier_notes | Text | (b) | | Carrier/admin |
| 114 | customer_notes | Text | (c) | | Buyer notes |
| 115 | has_exception | Check | (b) | | Admin flag |
| 116 | exception_type | Select | (b) | | Admin selects |
| 117 | exception_description | Small Text | (b) | | Admin writes |
| 118 | exception_resolved | Check | (b) | | Admin resolves |
| 119 | exception_resolution_date | Datetime | (a) | RO | System timestamp |

---

### 29. Shipping Rule
**Autoname:** field:rule_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | rule_name | Data | (b) | R, U | Admin/seller defines |
| 2 | rule_type | Select | (b) | R | Admin/seller selects |
| 3 | is_active | Check | (b) | | Admin/seller toggle |
| 4 | seller | Link | (c) | | Seller links self |
| 5 | tenant | Link | (b) | | Admin assigns |
| 6 | priority | Int | (b) | | Admin/seller config |
| 7 | description | Text | (b) | | Admin/seller writes |
| 8 | zones | Table | (b) | | Admin/seller config |
| 9 | calculation_method | Select | (b) | R | Admin/seller selects |
| 10 | base_rate | Currency | (b) | | Admin/seller config |
| 11 | per_kg_rate | Currency | (b) | | Admin/seller config |
| 12 | per_item_rate | Currency | (b) | | Admin/seller config |
| 13 | currency | Link | (b) | R | Admin/seller selects |
| 14 | price_includes_tax | Check | (b) | | Admin/seller toggle |
| 15 | tax_rate | Percent | (b) | | Admin/seller config |
| 16 | rate_tiers | Table | (b) | | Admin/seller config |
| 17 | free_shipping_enabled | Check | (b) | | Admin/seller toggle |
| 18 | free_shipping_threshold | Currency | (b) | | Admin/seller config |
| 19 | free_shipping_categories | Small Text | (b) | | Admin/seller config |
| 20 | free_shipping_items | Small Text | (b) | | Admin/seller config |
| 21 | min_order_amount | Currency | (b) | | Admin/seller config |
| 22 | max_order_amount | Currency | (b) | | Admin/seller config |
| 23 | min_weight | Float | (b) | | Admin/seller config |
| 24 | max_weight | Float | (b) | | Admin/seller config |
| 25 | handling_fee | Currency | (b) | | Admin/seller config |
| 26 | handling_fee_type | Select | (b) | | Admin/seller selects |
| 27 | packaging_fee | Currency | (b) | | Admin/seller config |
| 28 | insurance_rate | Percent | (b) | | Admin/seller config |
| 29 | estimated_days_min | Int | (b) | | Admin/seller config |
| 30 | estimated_days_max | Int | (b) | | Admin/seller config |
| 31 | express_available | Check | (b) | | Admin/seller toggle |
| 32 | express_surcharge | Currency | (b) | | Admin/seller config |
| 33 | express_days | Int | (b) | | Admin/seller config |
| 34 | apply_to_all_categories | Check | (b) | | Admin/seller toggle |
| 35 | allowed_categories | Small Text | (b) | | Admin/seller config |
| 36 | excluded_categories | Small Text | (b) | | Admin/seller config |
| 37 | default_carrier | Link | (b) | | Admin/seller selects |
| 38 | allowed_carriers | Small Text | (b) | | Admin/seller config |
| 39 | valid_from | Date | (b) | | Admin/seller enters |
| 40 | valid_to | Date | (b) | | Admin/seller enters |

---

### 30. Tracking Event
**Autoname:** naming_series TE-.YYYY.-.######

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | shipment | Link | (a) | R | System links shipment |
| 2 | tracking_number | Data | (a) | | System captures |
| 3 | carrier | Select | (a) | | System sets carrier |
| 4 | event_timestamp | Datetime | (a) | R | System timestamp |
| 5 | event_code | Data | (a) | | System from carrier |
| 6 | event_status | Select | (a) | | System sets status |
| 7 | event_type | Select | (a) | R | System sets type |
| 8 | event_description | Small Text | (a) | R | System description |
| 9 | is_milestone | Check | (a) | | System flag |
| 10 | severity | Select | (a) | | System sets |
| 11 | is_exception | Check | (a) | | System flag |
| 12 | exception_type | Select | (a) | | System sets |
| 13 | location_name | Data | (a) | | System from carrier |
| 14 | facility_name | Data | (a) | | System from carrier |
| 15 | facility_type | Select | (a) | | System sets |
| 16 | city | Data | (a) | | System from carrier |
| 17 | state | Data | (a) | | System from carrier |
| 18 | postal_code | Data | (a) | | System from carrier |
| 19 | country | Link | (a) | | System from carrier |
| 20 | latitude | Float | (a) | | System from carrier |
| 21 | longitude | Float | (a) | | System from carrier |
| 22 | location_type | Select | (a) | | System sets |
| 23 | is_origin | Check | (a) | | System flag |
| 24 | is_destination | Check | (a) | | System flag |
| 25 | address_line | Data | (a) | | System from carrier |
| 26 | signed_by | Data | (a) | | System captures |
| 27 | signature_image | Attach Image | (a) | | System captures |
| 28 | proof_of_delivery_image | Attach Image | (a) | | System captures |
| 29 | delivery_location_type | Select | (a) | | System sets |
| 30 | delivery_instructions | Small Text | (a) | | System from carrier |
| 31 | left_at | Data | (a) | | System from carrier |
| 32 | attempt_number | Int | (a) | | System counter |
| 33 | reason_code | Data | (a) | | System from carrier |
| 34 | reason_description | Small Text | (a) | | System from carrier |
| 35 | reschedule_date | Date | (a) | | System from carrier |
| 36 | next_action | Select | (a) | | System/carrier |
| 37 | carrier_event_code | Data | (a) | | System from carrier |
| 38 | carrier_event_description | Small Text | (a) | | System from carrier |
| 39 | carrier_status_code | Data | (a) | | System from carrier |
| 40 | raw_event_data | JSON | (a) | | System from API |
| 41 | estimated_delivery_date | Date | (a) | | System from carrier |
| 42 | estimated_delivery_time | Time | (a) | | System from carrier |
| 43 | weight_at_event | Float | (a) | | System from carrier |
| 44 | marketplace_order | Link | (a) | | System link |
| 45 | sub_order | Link | (a) | | System link |
| 46 | seller | Link | (a) | | System link |
| 47 | buyer | Link | (a) | | System link |
| 48 | tenant | Link | (a) | | System link |
| 49 | notification_sent | Check | (a) | | System flag |
| 50 | notification_type | Select | (a) | | System sets |
| 51 | notification_sent_at | Datetime | (a) | RO | System timestamp |
| 52 | notification_recipient | Data | (a) | | System sets |
| 53 | notification_status | Select | (a) | | System status |
| 54 | sms_sent | Check | (a) | | System flag |
| 55 | email_sent | Check | (a) | | System flag |
| 56 | push_sent | Check | (a) | | System flag |
| 57 | naming_series | Select | (a) | H | System naming |
| 58 | source | Select | (a) | | System sets source |
| 59 | synced_at | Datetime | (a) | RO | System timestamp |
| 60 | sync_id | Data | (a) | U | System dedup ID |

---

## APP: tradehub_marketing (9 DocTypes)

---

### 31. Campaign
**Autoname:** field:campaign_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | campaign_name | Data | (c) | R, U | Seller defines |
| 2 | seller | Link | (c) | R | Seller links self |
| 3 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 4 | tenant | Link | (a) | RO, FF:seller.tenant | Auto-filled |
| 5 | tenant_name | Data | (a) | RO, FF:seller.tenant_name | Auto-filled |
| 6 | status | Select | (b) | R | Admin/seller manages |
| 7 | campaign_type | Select | (c) | R | Seller selects |
| 8 | start_date | Date | (c) | R | Seller enters |
| 9 | end_date | Date | (c) | R | Seller enters |
| 10 | budget | Currency | (c) | | Seller enters |
| 11 | description | Text Editor | (c) | | Seller writes |
| 12 | target_audience | Select | (c) | | Seller selects |
| 13 | linked_coupons | Int | (a) | RO | System counter |
| 14 | spent_amount | Currency | (a) | RO | System calculated |
| 15 | remaining_budget | Currency | (a) | RO | System calculated |
| 16 | total_usage | Int | (a) | RO | System counter |
| 17 | unique_users | Int | (a) | RO | System counter |
| 18 | views_count | Int | (a) | RO | System counter |
| 19 | clicks_count | Int | (a) | RO | System counter |
| 20 | orders_count | Int | (a) | RO | System counter |
| 21 | revenue_generated | Currency | (a) | RO | System calculated |

---

### 32. Coupon
**Autoname:** field:coupon_code

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | coupon_code | Data | (c) | R, U | Seller defines |
| 2 | coupon_name | Data | (c) | R | Seller defines |
| 3 | seller | Link | (c) | R | Seller links self |
| 4 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 5 | tenant | Link | (a) | RO, FF:seller.tenant | Auto-filled |
| 6 | tenant_name | Data | (a) | RO, FF:seller.tenant_name | Auto-filled |
| 7 | campaign | Link | (c) | | Seller links campaign |
| 8 | campaign_name | Data | (a) | RO, FF:campaign.campaign_name | Auto-filled |
| 9 | status | Select | (a) | RO | System manages |
| 10 | coupon_type | Select | (c) | R | Seller selects |
| 11 | discount_type | Select | (c) | R | Seller selects |
| 12 | discount_value | Float | (c) | R | Seller enters |
| 13 | max_discount_amount | Currency | (c) | | Seller enters |
| 14 | min_order_amount | Currency | (c) | | Seller enters |
| 15 | start_date | Date | (c) | R | Seller enters |
| 16 | end_date | Date | (c) | R | Seller enters |
| 17 | usage_limit | Int | (c) | | Seller enters |
| 18 | per_user_limit | Int | (c) | | Seller enters |
| 19 | used_count | Int | (a) | RO | System counter |
| 20 | applicable_products | Table MultiSelect | (c) | | Seller selects |
| 21 | applicable_categories | Table MultiSelect | (c) | | Seller selects |
| 22 | description | Small Text | (c) | | Seller writes |

---

### 33. Group Buy
**Autoname:** naming_series GB-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | title | Data | (c) | R | Seller enters |
| 3 | listing | Link | (c) | R | Seller links listing |
| 4 | seller | Link | (c) | R | Seller links self |
| 5 | status | Select | (b) | R | Admin/seller manages |
| 6 | start_date | Datetime | (c) | R | Seller enters |
| 7 | end_date | Datetime | (c) | R | Seller enters |
| 8 | min_quantity | Int | (c) | R | Seller enters |
| 9 | max_quantity | Int | (c) | | Seller enters |
| 10 | current_quantity | Int | (a) | RO | System counter |
| 11 | participant_count | Int | (a) | RO | System counter |
| 12 | base_price | Currency | (c) | R | Seller enters |
| 13 | current_price | Currency | (a) | RO | System calculated |
| 14 | total_commitment_amount | Currency | (a) | RO | System calculated |
| 15 | average_price | Currency | (a) | RO | System calculated |
| 16 | tiers | Table | (c) | | Seller configures |
| 17 | description | Text Editor | (c) | | Seller writes |
| 18 | terms | Text Editor | (c) | | Seller writes |
| 19 | view_count | Int | (a) | RO | System counter |
| 20 | funded_at | Datetime | (a) | RO | System timestamp |
| 21 | completed_at | Datetime | (a) | RO | System timestamp |
| 22 | created_by | Link | (a) | RO | System captures |
| 23 | created_at | Datetime | (a) | RO | System timestamp |
| 24 | tenant | Link | (b) | | Admin assigns |

---

### 34. Group Buy Commitment
**Autoname:** naming_series GBC-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | group_buy | Link | (c) | R | User links group buy |
| 3 | buyer | Link | (c) | R | Buyer links self |
| 4 | status | Select | (b) | R | Admin/system manages |
| 5 | quantity | Int | (c) | R | Buyer enters |
| 6 | commitment_date | Datetime | (a) | RO | System timestamp |
| 7 | unit_price | Currency | (a) | RO | System calculated |
| 8 | total_amount | Currency | (a) | RO | System calculated |
| 9 | share_percent | Percent | (a) | RO | System calculated |
| 10 | price_locked | Check | (a) | RO | System flag |
| 11 | locked_at | Datetime | (a) | RO | System timestamp |
| 12 | contribution_factor | Float | (a) | RO | System calculated |
| 13 | discount_percent | Percent | (a) | RO | System calculated |
| 14 | cancelled_at | Datetime | (a) | RO | System timestamp |
| 15 | refunded_at | Datetime | (a) | RO | System timestamp |
| 16 | refund_amount | Currency | (a) | RO | System calculated |
| 17 | modified_count | Int | (a) | RO | System counter |
| 18 | notes | Small Text | (c) | | Buyer writes |

---

### 35. Group Buy Payment
**Autoname:** naming_series GBP-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | group_buy | Link | (a) | R | System links |
| 3 | commitment | Link | (a) | R | System links |
| 4 | buyer | Link | (a) | R | System captures |
| 5 | status | Select | (b) | R | Admin manages |
| 6 | amount | Currency | (c) | R | Payment amount |
| 7 | payment_method | Select | (c) | R | Buyer selects |
| 8 | payment_date | Datetime | (a) | RO | System timestamp |
| 9 | platform_fee | Currency | (a) | RO | System calculated |
| 10 | net_amount | Currency | (a) | RO | System calculated |
| 11 | processed_by | Link | (a) | RO | System captures |
| 12 | processed_at | Datetime | (a) | RO | System timestamp |
| 13 | settlement_reference | Data | (a) | RO | System from gateway |
| 14 | settled_at | Datetime | (a) | RO | System timestamp |
| 15 | refunded_at | Datetime | (a) | RO | System timestamp |
| 16 | refund_reference | Data | (a) | RO | System from gateway |
| 17 | transaction_id | Data | (c) | | From gateway |
| 18 | notes | Small Text | (b) | | Admin notes |

---

### 36. Storefront
**Autoname:** STORE-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | store_name | Data | (c) | R | Seller enters |
| 2 | seller | Link | (c) | R | Seller links self |
| 3 | status | Select | (b) | R | Admin manages |
| 4 | slug | Data | (c) | U | Seller enters URL slug |
| 5 | tagline | Data | (c) | | Seller enters |
| 6 | description | Text Editor | (c) | | Seller writes |
| 7 | logo | Attach Image | (c) | | Seller uploads |
| 8 | banner_image | Attach Image | (c) | | Seller uploads |
| 9 | favicon | Attach Image | (c) | | Seller uploads |
| 10 | theme_color | Color | (c) | | Seller picks |
| 11 | secondary_color | Color | (c) | | Seller picks |
| 12 | font_family | Select | (c) | | Seller selects |
| 13 | layout_type | Select | (c) | | Seller selects |
| 14 | show_categories | Check | (c) | | Seller toggle |
| 15 | show_featured | Check | (c) | | Seller toggle |
| 16 | show_reviews | Check | (c) | | Seller toggle |
| 17 | contact_email | Data | (c) | | Seller enters |
| 18 | contact_phone | Data | (c) | | Seller enters |
| 19 | social_facebook | Data | (c) | | Seller enters |
| 20 | social_instagram | Data | (c) | | Seller enters |
| 21 | social_twitter | Data | (c) | | Seller enters |
| 22 | social_linkedin | Data | (c) | | Seller enters |
| 23 | meta_title | Data | (c) | | Seller enters SEO |
| 24 | meta_description | Small Text | (c) | | Seller enters SEO |
| 25 | meta_keywords | Data | (c) | | Seller enters SEO |
| 26 | shipping_policy | Text Editor | (c) | | Seller writes |
| 27 | return_policy | Text Editor | (c) | | Seller writes |
| 28 | privacy_policy | Text Editor | (c) | | Seller writes |
| 29 | terms_of_service | Text Editor | (c) | | Seller writes |
| 30 | custom_css | Code | (c) | | Seller enters |
| 31 | custom_js | Code | (c) | | Seller enters |
| 32 | total_products | Int | (a) | RO | System counter |
| 33 | total_views | Int | (a) | RO | System counter |
| 34 | total_followers | Int | (a) | RO | System counter |
| 35 | average_rating | Float | (a) | RO | System calculated |
| 36 | total_reviews | Int | (a) | RO | System counter |
| 37 | total_sales | Int | (a) | RO | System counter |
| 38 | published_at | Datetime | (a) | RO | System timestamp |
| 39 | last_updated_at | Datetime | (a) | RO | System timestamp |
| 40 | created_by | Link | (a) | RO | System captures |
| 41 | modified_by | Link | (a) | RO | System captures |
| 42 | tenant | Link | (b) | | Admin assigns |

---

### 37. Subscription
**Autoname:** SUB-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | subscription_package | Link | (c) | R | Seller selects package |
| 2 | package_name | Data | (a) | RO, FF:subscription_package.package_name | Auto-filled |
| 3 | billing_period | Data | (a) | RO, FF:subscription_package.billing_period | Auto-filled |
| 4 | seller | Link | (c) | R | Seller links self |
| 5 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 6 | tenant | Link | (a) | RO, FF:seller.tenant | Auto-filled |
| 7 | tenant_name | Data | (a) | RO, FF:seller.tenant_name | Auto-filled |
| 8 | status | Select | (b) | R | Admin/system manages |
| 9 | start_date | Date | (c) | R | Set at subscription |
| 10 | next_billing_date | Date | (b) | | Admin can adjust |
| 11 | is_active | Check | (a) | RO | System flag |
| 12 | last_billing_date | Date | (a) | RO | System timestamp |
| 13 | cancellation_date | Date | (a) | RO | System timestamp |
| 14 | monthly_price | Currency | (b) | | Admin can override |
| 15 | currency | Data | (a) | RO, FF:subscription_package.currency | Auto-filled |
| 16 | total_billed | Currency | (a) | RO | System calculated |
| 17 | total_paid | Currency | (a) | RO | System calculated |
| 18 | outstanding_amount | Currency | (a) | RO | System calculated |
| 19 | grace_period_days | Int | (a) | RO, FF:subscription_package.grace_period_days | Auto-filled |
| 20 | auto_suspend_enabled | Check | (a) | RO, FF:subscription_package.auto_suspend_enabled | Auto-filled |
| 21 | grace_period_start_date | Date | (a) | RO | System timestamp |
| 22 | grace_period_end_date | Date | (a) | RO | System timestamp |
| 23 | in_grace_period | Check | (a) | RO | System flag |
| 24 | grace_period_warning_sent | Check | (a) | RO | System flag |
| 25 | suspension_warning_sent | Check | (a) | RO | System flag |
| 26 | is_suspended | Check | (a) | RO | System flag |
| 27 | suspended_at | Datetime | (a) | RO | System timestamp |
| 28 | last_reactivated_at | Datetime | (a) | RO | System timestamp |
| 29 | reactivation_count | Int | (a) | RO | System counter |
| 30 | renewal_reminder_sent | Check | (a) | RO | System flag |
| 31 | renewal_reminder_date | Date | (a) | RO | System timestamp |
| 32 | failed_renewal_attempts | Int | (a) | RO | System counter |
| 33 | last_renewal_attempt | Datetime | (a) | RO | System timestamp |
| 34 | renewal_failure_reason | Data | (a) | RO | System captures |
| 35 | max_products | Int | (a) | RO, FF:subscription_package.max_products | Auto-filled |
| 36 | max_orders_per_month | Int | (a) | RO, FF:subscription_package.max_orders_per_month | Auto-filled |
| 37 | max_api_calls_per_day | Int | (a) | RO, FF:subscription_package.max_api_calls_per_day | Auto-filled |
| 38 | has_analytics | Check | (a) | RO, FF:subscription_package.has_analytics | Auto-filled |
| 39 | has_priority_support | Check | (a) | RO, FF:subscription_package.has_priority_support | Auto-filled |
| 40 | has_api_access | Check | (a) | RO, FF:subscription_package.has_api_access | Auto-filled |
| 41 | has_bulk_import | Check | (a) | RO, FF:subscription_package.has_bulk_import | Auto-filled |
| 42 | has_advanced_reporting | Check | (a) | RO, FF:subscription_package.has_advanced_reporting | Auto-filled |
| 43 | commission_rate | Percent | (a) | RO, FF:subscription_package.commission_rate | Auto-filled |
| 44 | current_product_count | Int | (a) | RO | System counter |
| 45 | current_month_orders | Int | (a) | RO | System counter |
| 46 | current_day_api_calls | Int | (a) | RO | System counter |
| 47 | last_payment_date | Date | (a) | RO | System timestamp |
| 48 | last_payment_amount | Currency | (a) | RO | System captures |
| 49 | last_payment_method | Data | (a) | RO | System captures |
| 50 | payment_reference | Data | (a) | RO | System captures |
| 51 | previous_package | Link | (a) | RO | System link |
| 52 | upgrade_date | Date | (a) | RO | System timestamp |
| 53 | downgrade_date | Date | (a) | RO | System timestamp |
| 54 | prorate_amount | Currency | (a) | RO | System calculated |
| 55 | created_at | Datetime | (a) | RO | System timestamp |
| 56 | modified_at | Datetime | (a) | RO | System timestamp |
| 57 | created_by | Link | (a) | RO | System captures |
| 58 | modified_by | Link | (a) | RO | System captures |

---

### 38. Subscription Package
**Autoname:** field:package_name

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | package_name | Data | (b) | R, U | Admin defines |
| 2 | display_name | Data | (b) | R | Admin defines |
| 3 | status | Select | (b) | R | Admin manages |
| 4 | tier | Select | (b) | R | Admin selects |
| 5 | billing_period | Select | (b) | R | Admin selects |
| 6 | monthly_price | Currency | (b) | R | Admin sets price |
| 7 | annual_price | Currency | (b) | | Admin sets price |
| 8 | currency | Link | (b) | R | Admin selects |
| 9 | description | Text Editor | (b) | | Admin writes |
| 10 | max_products | Int | (b) | | Admin config |
| 11 | max_orders_per_month | Int | (b) | | Admin config |
| 12 | max_api_calls_per_day | Int | (b) | | Admin config |
| 13 | has_analytics | Check | (b) | | Admin toggle |
| 14 | has_priority_support | Check | (b) | | Admin toggle |
| 15 | has_api_access | Check | (b) | | Admin toggle |
| 16 | has_bulk_import | Check | (b) | | Admin toggle |
| 17 | has_advanced_reporting | Check | (b) | | Admin toggle |
| 18 | commission_rate | Percent | (b) | R | Admin sets |
| 19 | grace_period_days | Int | (b) | | Admin config |
| 20 | auto_suspend_enabled | Check | (b) | | Admin toggle |
| 21 | trial_days | Int | (b) | | Admin config |
| 22 | is_featured | Check | (b) | | Admin toggle |
| 23 | display_order | Int | (b) | | Admin config |
| 24 | subscriber_count | Int | (a) | RO | System counter |
| 25 | active_subscriber_count | Int | (a) | RO | System counter |
| 26 | total_revenue | Currency | (a) | RO | System calculated |
| 27 | last_calculated_at | Datetime | (a) | RO | System timestamp |
| 28 | created_at | Datetime | (a) | RO | System timestamp |
| 29 | modified_at | Datetime | (a) | RO | System timestamp |

---

### 39. Wholesale Offer
**Autoname:** naming_series WSO-.#####

| # | fieldname | fieldtype | Category | Patterns | Rationale |
|---|-----------|-----------|----------|----------|-----------|
| 1 | naming_series | Select | (a) | R, H | System naming |
| 2 | offer_code | Data | (a) | RO, U | System-generated |
| 3 | title | Data | (c) | R | Seller enters |
| 4 | seller | Link | (c) | R | Seller links self |
| 5 | seller_name | Data | (a) | RO, FF:seller.seller_name | Auto-filled |
| 6 | tenant | Link | (a) | RO, FF:seller.tenant | Auto-filled |
| 7 | tenant_name | Data | (a) | RO, FF:seller.tenant_name | Auto-filled |
| 8 | status | Select | (b) | R | Admin/seller manages |
| 9 | offer_type | Select | (c) | R | Seller selects |
| 10 | start_date | Date | (c) | R | Seller enters |
| 11 | end_date | Date | (c) | R | Seller enters |
| 12 | min_order_amount | Currency | (c) | | Seller enters |
| 13 | min_quantity | Int | (c) | | Seller enters |
| 14 | discount_type | Select | (c) | R | Seller selects |
| 15 | discount_value | Float | (c) | R | Seller enters |
| 16 | max_discount | Currency | (c) | | Seller enters |
| 17 | products | Table | (c) | | Seller configures |
| 18 | description | Text Editor | (c) | | Seller writes |
| 19 | terms | Text Editor | (c) | | Seller writes |
| 20 | usage_limit | Int | (c) | | Seller enters |
| 21 | total_products | Int | (a) | RO | System counter |
| 22 | total_quantity | Int | (a) | RO | System counter |
| 23 | total_value | Currency | (a) | RO | System calculated |
| 24 | current_usage | Int | (a) | RO | System counter |
| 25 | published_at | Datetime | (a) | RO | System timestamp |
| 26 | created_by | Link | (a) | RO | System captures |

---

## SUMMARY STATISTICS

### Per-App Category Breakdown

| App | DocTypes | (a) System | (b) Admin | (c) User | Total Fields |
|-----|----------|-----------|-----------|----------|-------------|
| tradehub_compliance | 23 | ~285 | ~195 | ~130 | ~610 |
| tradehub_logistics | 7 | ~215 | ~220 | ~175 | ~610 |
| tradehub_marketing | 9 | ~155 | ~75 | ~105 | ~335 |
| **TOTALS (3 apps)** | **39** | **~655** | **~490** | **~410** | **~1555** |

### Key Patterns Observed

1. **fetch_from + read_only**: ~120 instances across 3 apps. Always category (a).
2. **read_only without fetch_from**: ~80 instances. System-computed values, timestamps, counters.
3. **hidden naming_series**: 15 DocTypes use hidden naming_series. Always category (a).
4. **Password fields**: Found in Carrier (api_key, api_secret, webhook_secret) and Logistics Provider (api_key, api_secret, api_password, webhook_secret) and ESign Provider (api_secret). Always category (b).
5. **Audit-only DocTypes**: Consent Audit Log and Contract Revision have read-only permissions (no create/write for System Manager). All fields are category (a) despite read_only:0.
6. **Tracking Event**: Entirely system-generated DocType. All 60 fields are category (a).
7. **Tenant isolation**: Present in most DocTypes via tenant/tenant_name fields. Compliance uses both tenant and company.
8. **set_only_once**: Not found in any of these 39 DocTypes.
