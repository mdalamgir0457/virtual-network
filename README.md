# virtual-network
vitual network 
reated Resource Groups using for_each
✅ Deployed Multiple Virtual Networks
✅ Configured Address Spaces
✅ Connected VNets with corresponding Resource Groups dynamically


Terraform Code:

resource "azurerm_resource_group" "resource_group" {
  for_each = var.resource_name

  name     = each.key
  location = each.value
}

resource "azurerm_virtual_network" "vnet_3" {

  depends_on = [azurerm_resource_group.resource_group]

  for_each = var.vnet_name

  name = each.value.name

  location = azurerm_resource_group.resource_group[each.value.resource_group].location

  resource_group_name = azurerm_resource_group.resource_group[each.value.resource_group].name

  address_space = each.value.address_space
}

📂 terraform.tfvars

resource_name = {
  rg1 = "eastus"
  rg2 = "westus"
}

vnet_name = {

  vnet1 = {
    name            = "vnet_26may"
    resource_group  = "rg1"
    address_space   = ["10.0.0.0/16"]
  }

  vnet2 = {
    name            = "vnet_27may"
    resource_group  = "rg2"
    address_space   = ["20.0.0.0/16"]
  }
}

🌐 CIDR Used:

VNet1:
10.0.0.0/16

VNet2:
20.0.0.0/16

This hands-on practice improved my understanding of:
✔ Terraform for_each
✔ Dynamic Resource Mapping
✔ Azure Networking
✔ Infrastructure Automation
