# 先决条件：
* Global Azure AD：用于同步账户到Github， 并提供身份验证；
* Global Azure AD 全局管理员账户：用于配置单点登录
* Global Azure 订阅 ID：用于绑定到Github计费； 
* Azure 订阅管理员：用于配置Github 绑定Azure订阅；

# Github 创建EMU企业
1.	微软售前团队会负责和Github沟通，申请启用EMU企业组织；
2.	客户需提供shortcode （3-8个字符，该代码将用作企业成员用户名的后缀），和管理员邮箱；

# 配置EMU 管理员临时密码
1.	Github 启用EMU企业组织后，会发送激活邮件给到管理员邮箱；
2.	Github 会为EMU企业账户生成一个临时配置管理员，名称为：shortcode_admin
3.	管理员需根据邮箱中的指引，为临时配置管理员创建密码（临时的管理员账户为shortcode_admin）；
* 临时配置管理账户主要用于配置EMU企业组织和AAD集成；
* 请务必使用浏览器隐私模式来为临时管理员账户重置密码和登录；
* 配置了和Azure AD 账户同步后，临时配置管理账户将会失效。请确保下载了临时配置管理员的恢复密钥：
![alt text](image.png)

# 选择EMU 身份验证集成方案
| 功能需求 | Global Azure AD | 自建IDP | 说明 |
| SAML 2.0 | 已支持 | 必须 | 身份验证 |
| SCIM 2.0 | 已支持 | 必须 | 账户同步 |
| OIDC | 已支持 | 不支持 | 身份验证 |
| 公网访问 | 已支持 | 必须 | 接受Github身份验证请求 |
| 账户同步范围 | 可创建单独的Azure AD，无需将企业内部账户同步到Github | 将企业内部账户同步到Github（仅同步账户，密码无需同步） |  |
| 配置方式 | 内置了对Github的集成，配置简单，无需开发 | 需自建IDP提供商配合调试，可能需要二次开发 | 自建IDP 配置较为复杂，需IDP开发商积极配合 |

## 基于Azure AD 配置身份验证集成
1. 配置OIDC 集成：https://docs.github.com/zh/enterprise-cloud@latest/admin/identity-and-access-management/using-enterprise-managed-users-for-iam/configuring-oidc-for-enterprise-managed-users
2. 配置SCIM 集成：
* 在Github中生成账户同步的票据令牌：https://docs.github.com/zh/enterprise-cloud@latest/admin/identity-and-access-management/provisioning-user-accounts-for-enterprise-managed-users/configuring-scim-provisioning-for-enterprise-managed-users#%E5%88%9B%E5%BB%BA-personal-access-token
* 在Azure AD配置SCIM：https://learn.microsoft.com/en-us/azure/active-directory/saas-apps/github-enterprise-managed-user-oidc-provisioning-tutorial

## 基于自建IDP 配置身份验证集成
1. SSO 集成配置：https://docs.github.com/zh/enterprise-cloud@latest/admin/identity-and-access-management/iam-configuration-reference/saml-configuration-reference
2. SCIM 集成配置：https://docs.github.com/zh/enterprise-cloud@latest/admin/identity-and-access-management/provisioning-user-accounts-for-enterprise-managed-users/provisioning-users-and-groups-with-scim-using-the-rest-api

# 启用Github Copilot
1.	使用Github 企业管理员登录Github；
![alt text](image-1.png) 
2.	确认License 信息正确；
![alt text](image-2.png)
3.	将Github Enterprise Billing 绑定到Azure 订阅
此操作需Azure 订阅管理员权限；
https://docs.github.com/zh/billing/managing-billing-for-your-github-account/connecting-an-azure-subscription
![alt text](image-3.png)

4.	绑定订阅后，需在企业级别启用Copilot，参考如下文档：
https://docs.github.com/zh/enterprise-cloud@latest/admin/policies/enforcing-policies-for-your-enterprise/enforcing-policies-for-github-copilot-in-your-enterprise#enforcing-a-policy-to-manage-the-use-of-github-copilot-business-in-your-enterprise



