---
name: Security groups allowing public SSH
slug: sg-public-ssh
query: '{ securityGroups(where: {rules_SOME: {direction: \"Inbound\", action:
  \"Allow\", AND: [{OR: [{sources_INCLUDES: \"cidr:0.0.0.0/0\"},
  {sources_INCLUDES: \"cidr:::/0\"}, {sources_INCLUDES: \"tag:Internet\"},
  {sources: []}]}, {OR: [{sourceFromPort_LTE: 22, sourceToPort_GTE: 22}]}]}}) {
  identifier accountID cloudAccountID cloudAccountName cloudProvider
  idFromProvider internalAssetType internalName internalRegion assetCategory
  contentHash }}'
---
