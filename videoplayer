
<div ng-app="appDirectives">
	<div  class="CtrlBar_box col-md-12" ng-controller="QuoteFactory as factory" >

		<div anguvideo ng-model="factory.content" width="250" height="250"></div>
		<input style="color:#000;" type="text" ng-model="factory.content" />
	</div>	
</div>

<script type="text/javascript">

var module = angular.module("directives",[]);
angular.module('anguvideo', [])
.directive("anguvideo", ['$sce', function ($sce) {
    return {
        restrict: 'EA',
        scope: {
            source: '=ngModel',//= two way data binding
            width: '@',//@ one way data binding
            height: '@'//& function binding
        },
        replace: true,
        template: '<div class="anguvideo">' +
        '<iframe class="videoClass" type="text/html" width="{{width}}" height="{{height}}" ng-src="{{url}}" allowfullscreen frameborder="0"></iframe>' +
        '</div>',
        link: function (scope, element, attrs) {
            var embedFriendlyUrl = "",
                urlSections,
                index;
			var full = '',id = '',front = '';

			scope.$watch('source', function (url) {
                if (url) 
				{
					switch(true)
					{
						case (/^http[s]?\:\/\/(www\.youtube\.com)/).test(url):
							
							pos = url.indexOf("=");
							if(pos != -1)
							{
								id = url.substr(++pos);
								front = 'https://www.youtube.com/embed/' + id;
							}
							break;
							
						case (/^http[s]?\:\/\/(www\.facebook\.com)/).test(url):
							front = 'https://www.facebook.com/plugins/video.php?href=' + url;
							break;
							
						case (/^http[s]?\:\/\/(vimeo\.com)/).test(url):

							pos = url.lastIndexOf("/");
							if(pos != -1)
							{
								id = url.substr(++pos);
								front = 'https://player.vimeo.com/video/'+ id;
							}
							
							break;
							
						case (/^http[s]?\:\/\/(www\.kickstarter\.com)/).test(url):
							dirtyIndex = url.lastIndexOf('?');
							dirty = url.substr(dirtyIndex);
							console.log(dirty);
							urlc = url.replace(dirty,'');
							front = urlc + '/widget/video.html';
							break;
						
						case (/^http[s]?\:\/\/(www\.instagram\.com)/).test(url):
							
							dirtyIndex = url.indexOf('?');
							dirty = url.substr(dirtyIndex);
							urlc = url.replace(dirty,'');
							front = urlc +'embed/';
							break;
						
						default:
							front =  "";
							break;
					}

					(front != '')?full = front :full = "the url is not contain video";
					console.log(front);
					console.log(full);
					scope.url =$sce.trustAsResourceUrl(full);
                }
            });
        }
    };
}]);

var appDirectives = angular.module('appDirectives',['directives','ngSanitize',"anguvideo"]);

appDirectives.factory('Scopes', function ($rootScope) {
    var mem = {};
 
    return {
        store: function (key, value) {
            mem[key] = value;
        },
        get: function (key) {
            return mem[key];
        }
    };
});

appDirectives.controller('QuoteFactory', function($scope, $http, $sce, Scopes ) {

	var factory = this;
});


</script>
