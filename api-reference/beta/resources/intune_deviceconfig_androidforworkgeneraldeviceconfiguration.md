﻿# androidForWorkGeneralDeviceConfiguration resource type

> **Important:** APIs under the / beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

> **Note:** Using the Microsoft Graph APIs to configure Intune controls and policies still requires that the Intune service is [correctly licensed](https://go.microsoft.com/fwlink/?linkid=839381) by the customer.

Android For Work general device configuration.

Inherits from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)

## Methods
|Method|Return Type|Description|
|:---|:---|:---|
|[List androidForWorkGeneralDeviceConfigurations](../api/intune_deviceconfig_androidforworkgeneraldeviceconfiguration_list.md)|[androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md) collection|List properties and relationships of the [androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md) objects.|
|[Get androidForWorkGeneralDeviceConfiguration](../api/intune_deviceconfig_androidforworkgeneraldeviceconfiguration_get.md)|[androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md)|Read properties and relationships of the [androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md) object.|
|[Create androidForWorkGeneralDeviceConfiguration](../api/intune_deviceconfig_androidforworkgeneraldeviceconfiguration_create.md)|[androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md)|Create a new [androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md) object.|
|[Delete androidForWorkGeneralDeviceConfiguration](../api/intune_deviceconfig_androidforworkgeneraldeviceconfiguration_delete.md)|None|Deletes a [androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md).|
|[Update androidForWorkGeneralDeviceConfiguration](../api/intune_deviceconfig_androidforworkgeneraldeviceconfiguration_update.md)|[androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md)|Update the properties of a [androidForWorkGeneralDeviceConfiguration](../resources/intune_deviceconfig_androidforworkgeneraldeviceconfiguration.md) object.|

## Properties
|Property|Type|Description|
|:---|:---|:---|
|id|String|Key of the entity. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|lastModifiedDateTime|DateTimeOffset|DateTime the object was last modified. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|roleScopeTagIds|String collection|List of Scope Tags for this Entity instance. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|supportsScopeTags|Boolean|Indicates whether or not the underlying Device Configuration supports the assignment of scope tags. Assigning to the ScopeTags property is not allowed when this value is false and entities will not be visible to scoped users. This occurs for Legacy policies created in Silverlight and can be resolved by deleting and recreating the policy in the Azure Portal. This property is read-only. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|createdDateTime|DateTimeOffset|DateTime the object was created. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|description|String|Admin provided description of the Device Configuration. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|displayName|String|Admin provided name of the device configuration. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|version|Int32|Version of the device configuration. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|passwordBlockFingerprintUnlock|Boolean|Indicates whether or not to block fingerprint unlock.|
|passwordBlockTrustAgents|Boolean|Indicates whether or not to block Smart Lock and other trust agents.|
|passwordExpirationDays|Int32|Number of days before the password expires. Valid values 1 to 365|
|passwordMinimumLength|Int32|Minimum length of passwords. Valid values 4 to 16|
|passwordMinutesOfInactivityBeforeScreenTimeout|Int32|Minutes of inactivity before the screen times out.|
|passwordPreviousPasswordBlockCount|Int32|Number of previous passwords to block. Valid values 0 to 24|
|passwordSignInFailureCountBeforeFactoryReset|Int32|Number of sign in failures allowed before factory reset. Valid values 4 to 11|
|passwordRequiredType|[androidForWorkRequiredPasswordType](../resources/intune_deviceconfig_androidforworkrequiredpasswordtype.md)|Type of password that is required. Possible values are: `deviceDefault`, `lowSecurityBiometric`, `required`, `atLeastNumeric`, `numericComplex`, `atLeastAlphabetic`, `atLeastAlphanumeric`, `alphanumericWithSymbols`.|
|workProfileDataSharingType|[androidForWorkCrossProfileDataSharingType](../resources/intune_deviceconfig_androidforworkcrossprofiledatasharingtype.md)|Type of data sharing that is allowed. Possible values are: `deviceDefault`, `preventAny`, `allowPersonalToWork`, `noRestrictions`.|
|workProfileBlockNotificationsWhileDeviceLocked|Boolean|Indicates whether or not to block notifications while device locked.|
|workProfileBlockAddingAccounts|Boolean|Block users from adding/removing accounts in work profile.|
|workProfileBluetoothEnableContactSharing|Boolean|Allow bluetooth devices to access enterprise contacts.|
|workProfileBlockScreenCapture|Boolean|Block screen capture in work profile.|
|workProfileBlockCrossProfileCallerId|Boolean|Block display work profile caller ID in personal profile.|
|workProfileBlockCamera|Boolean|Block work profile camera.|
|workProfileBlockCrossProfileContactsSearch|Boolean|Block work profile contacts availability in personal profile.|
|workProfileBlockCrossProfileCopyPaste|Boolean|Boolean that indicates if the setting disallow cross profile copy/paste is enabled.|
|workProfileDefaultAppPermissionPolicy|[androidForWorkDefaultAppPermissionPolicyType](../resources/intune_deviceconfig_androidforworkdefaultapppermissionpolicytype.md)|Type of password that is required. Possible values are: `deviceDefault`, `prompt`, `autoGrant`, `autoDeny`.|
|workProfilePasswordBlockFingerprintUnlock|Boolean|Indicates whether or not to block fingerprint unlock for work profile.|
|workProfilePasswordBlockTrustAgents|Boolean|Indicates whether or not to block Smart Lock and other trust agents for work profile.|
|workProfilePasswordExpirationDays|Int32|Number of days before the work profile password expires. Valid values 1 to 365|
|workProfilePasswordMinimumLength|Int32|Minimum length of work profile password. Valid values 4 to 16|
|workProfilePasswordMinNumericCharacters|Int32|Minimum # of numeric characters required in work profile password. Valid values 1 to 10|
|workProfilePasswordMinNonLetterCharacters|Int32|Minimum # of non-letter characters required in work profile password. Valid values 1 to 10|
|workProfilePasswordMinLetterCharacters|Int32|Minimum # of letter characters required in work profile password. Valid values 1 to 10|
|workProfilePasswordMinLowerCaseCharacters|Int32|Minimum # of lower-case characters required in work profile password. Valid values 1 to 10|
|workProfilePasswordMinUpperCaseCharacters|Int32|Minimum # of upper-case characters required in work profile password. Valid values 1 to 10|
|workProfilePasswordMinSymbolCharacters|Int32|Minimum # of symbols required in work profile password. Valid values 1 to 10|
|workProfilePasswordMinutesOfInactivityBeforeScreenTimeout|Int32|Minutes of inactivity before the screen times out.|
|workProfilePasswordPreviousPasswordBlockCount|Int32|Number of previous work profile passwords to block. Valid values 0 to 24|
|workProfilePasswordSignInFailureCountBeforeFactoryReset|Int32|Number of sign in failures allowed before work profile is removed and all corporate data deleted. Valid values 4 to 11|
|workProfilePasswordRequiredType|[androidForWorkRequiredPasswordType](../resources/intune_deviceconfig_androidforworkrequiredpasswordtype.md)|Type of work profile password that is required. Possible values are: `deviceDefault`, `lowSecurityBiometric`, `required`, `atLeastNumeric`, `numericComplex`, `atLeastAlphabetic`, `atLeastAlphanumeric`, `alphanumericWithSymbols`.|
|workProfileRequirePassword|Boolean|Password is required or not for work profile|
|securityRequireVerifyApps|Boolean|Require the Android Verify apps feature is turned on.|
|vpnAlwaysOnPackageIdentifier|String|Enable lockdown mode for always-on VPN.|
|vpnEnableAlwaysOnLockdownMode|Boolean|Enable lockdown mode for always-on VPN.|

## Relationships
|Relationship|Type|Description|
|:---|:---|:---|
|groupAssignments|[deviceConfigurationGroupAssignment](../resources/intune_deviceconfig_deviceconfigurationgroupassignment.md) collection|The list of group assignments for the device configuration profile. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|assignments|[deviceConfigurationAssignment](../resources/intune_deviceconfig_deviceconfigurationassignment.md) collection|The list of assignments for the device configuration profile. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|deviceStatuses|[deviceConfigurationDeviceStatus](../resources/intune_deviceconfig_deviceconfigurationdevicestatus.md) collection|Device configuration installation status by device. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|userStatuses|[deviceConfigurationUserStatus](../resources/intune_deviceconfig_deviceconfigurationuserstatus.md) collection|Device configuration installation status by user. Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|deviceStatusOverview|[deviceConfigurationDeviceOverview](../resources/intune_deviceconfig_deviceconfigurationdeviceoverview.md)|Device Configuration devices status overview Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|userStatusOverview|[deviceConfigurationUserOverview](../resources/intune_deviceconfig_deviceconfigurationuseroverview.md)|Device Configuration users status overview Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|
|deviceSettingStateSummaries|[settingStateDeviceSummary](../resources/intune_deviceconfig_settingstatedevicesummary.md) collection|Device Configuration Setting State Device Summary Inherited from [deviceConfiguration](../resources/intune_deviceconfig_deviceconfiguration.md)|

## JSON Representation
Here is a JSON representation of the resource.
<!-- {
  "blockType": "resource",
  "keyProperty": "id",
  "@odata.type": "microsoft.graph.androidForWorkGeneralDeviceConfiguration"
}
-->
``` json
{
  "@odata.type": "#microsoft.graph.androidForWorkGeneralDeviceConfiguration",
  "id": "String (identifier)",
  "lastModifiedDateTime": "String (timestamp)",
  "roleScopeTagIds": [
    "String"
  ],
  "supportsScopeTags": true,
  "createdDateTime": "String (timestamp)",
  "description": "String",
  "displayName": "String",
  "version": 1024,
  "passwordBlockFingerprintUnlock": true,
  "passwordBlockTrustAgents": true,
  "passwordExpirationDays": 1024,
  "passwordMinimumLength": 1024,
  "passwordMinutesOfInactivityBeforeScreenTimeout": 1024,
  "passwordPreviousPasswordBlockCount": 1024,
  "passwordSignInFailureCountBeforeFactoryReset": 1024,
  "passwordRequiredType": "String",
  "workProfileDataSharingType": "String",
  "workProfileBlockNotificationsWhileDeviceLocked": true,
  "workProfileBlockAddingAccounts": true,
  "workProfileBluetoothEnableContactSharing": true,
  "workProfileBlockScreenCapture": true,
  "workProfileBlockCrossProfileCallerId": true,
  "workProfileBlockCamera": true,
  "workProfileBlockCrossProfileContactsSearch": true,
  "workProfileBlockCrossProfileCopyPaste": true,
  "workProfileDefaultAppPermissionPolicy": "String",
  "workProfilePasswordBlockFingerprintUnlock": true,
  "workProfilePasswordBlockTrustAgents": true,
  "workProfilePasswordExpirationDays": 1024,
  "workProfilePasswordMinimumLength": 1024,
  "workProfilePasswordMinNumericCharacters": 1024,
  "workProfilePasswordMinNonLetterCharacters": 1024,
  "workProfilePasswordMinLetterCharacters": 1024,
  "workProfilePasswordMinLowerCaseCharacters": 1024,
  "workProfilePasswordMinUpperCaseCharacters": 1024,
  "workProfilePasswordMinSymbolCharacters": 1024,
  "workProfilePasswordMinutesOfInactivityBeforeScreenTimeout": 1024,
  "workProfilePasswordPreviousPasswordBlockCount": 1024,
  "workProfilePasswordSignInFailureCountBeforeFactoryReset": 1024,
  "workProfilePasswordRequiredType": "String",
  "workProfileRequirePassword": true,
  "securityRequireVerifyApps": true,
  "vpnAlwaysOnPackageIdentifier": "String",
  "vpnEnableAlwaysOnLockdownMode": true
}
```





