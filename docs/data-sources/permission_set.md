---
page_title: "morpheus_permission_set Data Source - terraform-provider-morpheus"
subcategory: ""
description: |-
  Provides a Morpheus permission set data source.
---

# morpheus_permission_set (Data Source)

Provides a Morpheus permission set data source.

## Example Usage

```terraform
data "morpheus_group" "demo" {
  name = "Demo"
}

data "morpheus_instance_type" "demo" {
  name = "Demo"
}

data "morpheus_blueprint" "demo" {
  name = "Demo"
}

data "morpheus_catalog_item_type" "demo" {
  name = "Demo"
}

data "morpheus_vdi_pool" "demo" {
  name = "Demo"
}

data "morpheus_task" "demo" {
  name = "Demo"
}

data "morpheus_workflow" "demo" {
  name = "Demo"
}

data "morpheus_permission_set" "source_one" {
  override_permission_sets = [
    data.morpheus_permission_set.override_set.json,
  ]
  default_group_permission             = "full"
  default_instance_type_permission     = "none"
  default_blueprint_permission         = "none"
  default_report_type_permission       = "full"
  default_persona                      = "vdi"
  default_catalog_item_type_permission = "full"
  default_vdi_pool_permission          = "full"
  default_workflow_permission          = "full"
  default_task_permission              = "full"

  feature_permission {
    code   = "provisioning-admin"
    access = "full"
  }

  group_permission {
    id     = data.morpheus_group.demo.id
    access = "full"
  }

  instance_type_permission {
    id     = data.morpheus_instance_type.demo.id
    access = "full"
  }

  blueprint_permission {
    id     = data.morpheus_blueprint.demo.id
    access = "full"
  }

  report_type_permission {
    code   = "guidance"
    access = "full"
  }

  persona_permission {
    code   = "standard"
    access = "full"
  }

  persona_permission {
    code   = "serviceCatalog"
    access = "none"
  }

  catalog_item_type_permission {
    id     = data.morpheus_catalog_item_type.demo.id
    access = "full"
  }

  vdi_pool_permission {
    id     = data.morpheus_vdi_pool.demo.id
    access = "full"
  }

  workflow_permission {
    id     = data.morpheus_workflow.demo.id
    access = "full"
  }

  task_permission {
    id     = data.morpheus_task.demo.id
    access = "none"
  }
}

data "morpheus_permission_set" "override_set" {
  default_task_permission = "none"
  default_persona         = "standard"
  workflow_permission {
    id     = 2
    access = "full"
  }
  workflow_permission {
    id     = 11
    access = "full"
  }
  group_permission {
    id     = 1
    access = "read"
  }
}
```

<!-- schema generated by tfplugindocs -->
## Schema

### Optional

- `blueprint_permission` (Block List) The blueprint permissions associated with the user role (see [below for nested schema](#nestedblock--blueprint_permission))
- `catalog_item_type_permission` (Block List) The catalog item type permissions associated with the user role (see [below for nested schema](#nestedblock--catalog_item_type_permission))
- `default_blueprint_permission` (String) The default role permission for blueprints (none, full)
- `default_catalog_item_type_permission` (String) The default role permission for catalog item types (none, full)
- `default_group_permission` (String) The default role permission for groups (none, read, full)
- `default_instance_type_permission` (String) The default role permission for instance types (none, full)
- `default_persona` (String) The default role persona (standard, serviceCatalog, vdi)
- `default_persona_permission` (String) The default role permission for personas (none, full)
- `default_report_type_permission` (String) The default role permission for report types (none, full)
- `default_task_permission` (String) The default role permission for tasks (none, full)
- `default_vdi_pool_permission` (String) The default role permission for vdi pools (none, full)
- `default_workflow_permission` (String) The default role permission for workflows (none, full)
- `feature_permission` (Block List) The feature permissions associated with the user role (see [below for nested schema](#nestedblock--feature_permission))
- `group_permission` (Block List) The group permissions associated with the user role (see [below for nested schema](#nestedblock--group_permission))
- `instance_type_permission` (Block List) The instance type permissions associated with the user role (see [below for nested schema](#nestedblock--instance_type_permission))
- `override_permission_sets` (List of String) List of permission sets that are merged together into the exported json. In merging, the last permission applied in the list order is used. Non-overriding permissions will be added to the exported json.
- `persona_permission` (Block List) The persona permissions associated with the user role (see [below for nested schema](#nestedblock--persona_permission))
- `report_type_permission` (Block List) The report type permissions associated with the user role (see [below for nested schema](#nestedblock--report_type_permission))
- `task_permission` (Block List) The task permissions associated with the user role (see [below for nested schema](#nestedblock--task_permission))
- `vdi_pool_permission` (Block List) The vdi pool permissions associated with the user role (see [below for nested schema](#nestedblock--vdi_pool_permission))
- `workflow_permission` (Block List) The workflow permissions associated with the user role (see [below for nested schema](#nestedblock--workflow_permission))

### Read-Only

- `id` (String) The ID of this resource.
- `json` (String) JSON permission set rendered based on the arguments defined

<a id="nestedblock--blueprint_permission"></a>
### Nested Schema for `blueprint_permission`

Optional:

- `access` (String) The level of access granted to the blueprint (default, full, none)
- `id` (Number) The id of the blueprint


<a id="nestedblock--catalog_item_type_permission"></a>
### Nested Schema for `catalog_item_type_permission`

Optional:

- `access` (String) The level of access granted to the catalog item type (default, full, none)
- `id` (Number) The id of the catalog item type


<a id="nestedblock--feature_permission"></a>
### Nested Schema for `feature_permission`

Optional:

- `access` (String) The level of access granted to the feature permission (full, full_decrypted, group, listfiles, managerules, no, none, provision, read, rolemappings, user, view, yes)
- `code` (String) The code of the feature permission


<a id="nestedblock--group_permission"></a>
### Nested Schema for `group_permission`

Optional:

- `access` (String) The level of access granted to the group (default, full, none)
- `id` (Number) The id of the group


<a id="nestedblock--instance_type_permission"></a>
### Nested Schema for `instance_type_permission`

Optional:

- `access` (String) The level of access granted to the workflow (default, full, none)
- `id` (Number) The id of the instance type


<a id="nestedblock--persona_permission"></a>
### Nested Schema for `persona_permission`

Optional:

- `access` (String) The level of access granted to the persona (default, full, none)
- `code` (String) The code of the persona (standard, vdi, serviceCatalog)


<a id="nestedblock--report_type_permission"></a>
### Nested Schema for `report_type_permission`

Optional:

- `access` (String) The level of access granted to the report type (default, full, none)
- `code` (String) The report type code


<a id="nestedblock--task_permission"></a>
### Nested Schema for `task_permission`

Optional:

- `access` (String) The level of access granted to the task (default, full, none)
- `id` (Number) The id of the task


<a id="nestedblock--vdi_pool_permission"></a>
### Nested Schema for `vdi_pool_permission`

Optional:

- `access` (String) The level of access granted to the vdi pool (default, full, none)
- `id` (Number) The id of the vdi pool


<a id="nestedblock--workflow_permission"></a>
### Nested Schema for `workflow_permission`

Optional:

- `access` (String) The level of access granted to the workflow (default, full, none)
- `id` (Number) The id of the workflow