// WORK AROUND FOR INTERNET EXPLORER
(function() {

    // add this to the THREE vars
    THREE.noVideoTextureSupport = true; //SET THIS VALUE TO TRUE FOR IE

    // replace the videoTexture function
    THREE.VideoTexture = (function() {
        var _videoTexture = THREE.VideoTexture;
        var _ieVideoTexture = function(video, mapping, wrapS, wrapT, magFilter, minFilter, format, type, anisotropy) {
            if (THREE.noVideoTextureSupport) {
                var scope = this;

                scope.video = video;
                scope.ctx2d = document.createElement('canvas').getContext('2d');
                var canvas = scope.ctx2d.canvas;
                canvas.width = video.width;
                canvas.height = video.height;

                scope.ctx2d.drawImage(scope.video, 0, 0, scope.width, scope.height);
                THREE.Texture.call(scope, scope.ctx2d.canvas, mapping, wrapS, wrapT, magFilter, minFilter, format, type, anisotropy);

                scope.generateMipmaps = false;

                function update() {
                    requestAnimationFrame( update );
                    if (video.readyState >= video.HAVE_CURRENT_DATA) {
                        scope.ctx2d.drawImage(scope.video, 0, 0, scope.video.width, scope.video.height);
                        scope.needsUpdate = true;
                    }
                }

                update();
            }
        };
        return (THREE.noVideoTextureSupport ? _ieVideoTexture : _videoTexture);
    })();

    THREE.VideoTexture.prototype = Object.create(THREE.Texture.prototype);
    THREE.VideoTexture.prototype.constructor = THREE.VideoTexture;

})();