## Example

```
// composer
composer require muffin/trash
```

```php
// bootstrap.php
Plugin::load('Muffin/Trash');
```

```php
// in the initialize() method
$this->addBehavior('Muffin/Trash.Trash', [
    'field' => 'deleted',
	'events' => ['Articles.beforeFind']
]);
```

```php
// e.g index deleted is null
public function index()
{
	$query = $this->Articles
		->find()
		->where([
			'Articles.deleted IS' => NULL
		]);
}
```

```php
// e.g find('onlyTrashed')
public function onlyTrashed()
{
	$query = $this->Articles->find('onlyTrashed');
		
	$trash = $this->Articles
		->find('onlyTrashed')
		->count();
}
```

```php
// e.g trash()
// in controller
public function trash($id = null)
{
	$article = $this->Articles->get($id);
	...
	if ($this->Articles->trash($article)) {
		$this->Flash->success(__('The article has been trashed.'));
	}
	...
}
// in template
$this->Html->link(__('Trash'), ['action' => 'trash', $article->id])
```

```php
// e.g restoreTrash()
// in controller
public function restoreTrash($id = null)
{
	$article = $this->Articles->get($id);
	...
	if ($this->Articles->restoreTrash($article)) {
		$this->Flash->success(__('The article has been restores.'));
	}
	...
}
// in template
$this->Html->link(__('Restore'), ['action' => 'restoreTrash', $article->id])
```
