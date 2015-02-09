# Angular Bootstrap page size changer directive

A lightweight pagination directive that is focused on ... changing page size. It was not covered by [UI Bootstrap](http://angular-ui.github.io/bootstrap/) so here it is.

With this and the pagination directive you can have a complete server side paging with Angular.

## Settings

Settings can be provided as attributes in the `<sl-page-size-changer>` :

 * `ng-model` (mandatory) : Maximum number of items per page. You'll have to initialize it.

 * `ng-change` (mandatory for now) : Will be called when the itemsPerPage (ngModel) change.

 * `total-items` (default NULL) : Total number of items in all pages.

 * `items-per-page-list` (mandatory) : Array of all page sizes.

## Usage

### Controller

```javascript
angular.module('myApp', ['seblucas.slPageSizeChanger'])
.controller('demoCtrl', ['$scope', 'myDataService', function($scope, myDataService) {
    $scope.itemsPerPage = 48;
    $scope.itemsPerPageList = [24, 48, 96, 192];
    $scope.maxSize = 10;
    $scope.currentPage = 1;
    $scope.list = [];

    $scope.pageChanged = function() {
      myDataService.query()
                   .then(function(result) {
        $scope.totalItems = result.totalItems;
        $scope.list = result.list;
      });
    };

    $scope.pageChanged ();
  }]);
```

### View

```html
<h1>Title</h1>
<pagination total-items="totalItems" items-per-page="itemsPerPage" max-size="maxSize" ng-model="currentPage" ng-change="pageChanged()"></pagination>
<sl-page-size-changer total-items="totalItems" ng-model="itemsPerPage" ng-change="pageChanged()" items-per-page-list="itemsPerPageList"></sl-page-size-changer>
<br />
<div class="row" ng-repeat="item in list">
{{item.name}}
</div>
```

## License

Licensed under MIT.