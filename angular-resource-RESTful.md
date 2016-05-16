---
title: angular resource RESTful
date: 2016-04-09 10:14:42
tags: angular
---

# type 1: Controller

    app.controller('ProductIndexCtrl',
        function($scope, $resource, $q, $stateParams, productService) {
            $q.all([
                productService.query({
                    product_id: $stateParams.id
                }).$promise

Update

    productService.update({product_id: product_id},{product: product})

Create

    productService.create({},{product: product})

# type 1: Service

    angular.module('productModule', [])
        .service('productService', function($resource, $http) {
                var product = $resource('/api/v1/products/:product_id', {
                    product_id: '@product_id',
                }, {
                     update: { method:'PUT' },
                     create: { method: 'POST' },
                     delete: { method: 'DELETE'}
                });
                return product;
            }
        );

# type 2: controller

    app.controller('BanksBaseCtrl', function($scope, $resource, $q, bankService, $auth, $http) {
        $scope.BankService = new bankService();
    });

    app.controller('BanksIndexCtrl', function($rootScope, $scope, $http, $resource, $q, bankService, $auth) {
          $q.all([$scope.BankService.all().$promise]).then(function(ret){
            $scope.banks = ret[0]
        }
    });




# type 2(Verbosed mode): Service side

    angular.module('bankModule', [])
        .service('bankService', function($resource, $http) {
            var Bank;
            return Bank = (function() {
                function Bank(BankListId, errorHandler) {
                    var defaults;
                    this.service = $resource('/api/v1/banks/:id',
                    {
                        id: '@id'
                    },
                    {
                        update: {method: 'PUT'},
                        delete: { method: 'DELETE', params: {id: '@id'} },
                        create: { method: 'POST', params: {bank: '@bank'} }
                    });
                    this.errorHandler = errorHandler;
                    defaults = $http.defaults.headers;
                    defaults.patch = defaults.patch || {};
                    defaults.patch['Content-Type'] = 'application/json';
                }
                Bank.prototype.all = function() {
                    return this.service.query((function() {
                        return null;
                    }), this.errorHandler);
                };
                Bank.prototype.create = function(bank) {
                    return new this.service({
                        Bank: bank
                    }).$create((function() {
                        return null;
                    }), this.errorHandler);
                };
                Bank.prototype.update = function(bank, bank_id) {
                    return new this.service({
                        Bank: bank
                    }).$update({
                        id: bank_id
                    }, (function() {
                        return null;
                    }), this.errorHandler);
                };
                Bank.prototype.get = function(id){
                    return this.service.get({id: id}, (function() {
                        return null;
                    }), this.errorHandler);
                }
                Bank.prototype.delete = function(id){
                    return this.service.delete({id: id}, (function() {
                        return null;
                    }), this.errorHandler);
                }
                return Bank;
            })();
        });
