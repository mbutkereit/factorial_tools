# factorial_tools
Drupal Module that provides various commonly used helper functions

# Usage

## 1. Mass entity delete
To delete all entities of particular type use `factorial_tools_entities_delete()`

*Examples*
```php
/**
 * Delete all nodes.
 */
function mysite_deploy_update_8001(&$sandbox) {
  return factorial_tools_entities_delete($sandbox, 'node');
}

/**
 * Delete all published nodes of type article.
 */
function mysite_deploy_update_8002(&$sandbox) {
  $conditions = [
   ['status', 1],
   ['type', 'article'],
  ];
  return factorial_tools_entities_delete($sandbox, 'node', $conditions);
}

/**
 * Delete all users except uid 0 and uid 1.
 */
function mysite_deploy_update_8003(&$sandbox) {
  $conditions = [
   ['uid', [0,1], 'NOT IN'],
  ];
  return factorial_tools_entities_delete($sandbox, 'user', $conditions);
}
```

*Optionally we have a helper function to delete entities by providing an entityQuery,*

```php
/**
 * Delete all users except Anonymous and Super Admin.
 */
function mysite_deploy_update_8004(&$sandbox) {
  $query = \Drupal::entityQuery('user');
  $query->condition('uid', [0,1], 'NOT IN');
  return factorial_tools_entities_delete_by_query($sandbox, $query);
}
```

