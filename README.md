# Angular

Difference between $http and $q
-----
a) $http executes HTTP requests in an asynchronous manner, which means that you can not be sure about the time when you'll get an answer from the server. $q is a service that provides you the capability to execute multiple asynchronous tasks one after another. That being said they conceptionally do have nothing in common.


b) Consider a situation where you want to have multiple async HTTP calls to a server. You may have the possibility to nest each of those calls (for instance making the 2nd call in the success callback of the first call). However you find yourself in situations where you have various amounts of calls. You would then use $q to circumvent nesting code.


c) Whenever you have a single HTTP call you should use $http. Whenever you have numerous calls, you should use $q.


```function getSearchData() {
    return {
        // returns a promise for an object like:
        // { abo: resultFromAbo, ser: resultFromSer, ... }
        loadDataFromUrls: function () {
            var apiList = ["abo", "ser", "vol", "con", "giv", "blo", "par"];

            return $q.all(apiList.map(function (item) {
                return $http({
                    method: 'GET',
                    url: '/api/' + item
                });
            }))
            .then(function (results) {
                var resultObj = {};
                results.forEach(function (val, i) {
                    resultObj[apiList[i]] = val.data;
                });
                return resultObj;        
            });
        }
    };
}
```
Decorators In Angular
--------
<a href="https://toddmotto.com/angular-decorators">click here</a>

### <a href="https://www.toptal.com/angular-js/top-18-most-common-angularjs-developer-mistakes"> 18 Mistakes in AngularJs </a>
