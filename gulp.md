---
title: gulp
date: 2016-04-09 10:14:42
tags: javascript
---


// const build = require("public/plugin/v1/src/build_cfg.js");

// gulp.task("build", function (callback) {
//     build({ some: "public/plugin/v1/src/" }, 
//         callback);
// });

    // rjs({
    //     name: 'main',
    //     baseUrl: 'dist/js',
    //     out: 'carecadets.min.js'
    // })
gulp.task('build-plugin', function(){
    rjs({
        name: "main",
        baseUrl: export_cfg.src_dir,
        findNestedDependencies: true,
        include: true,
        wrap: true,
        removeCombined: true,
        allowSourceOverwrites: true,
        preserveLicenseComments: false,
        // paths: {
        //     requireLib: './require'
        // },
        out    : export_cfg.name
    })
    .pipe(gulp.dest(export_cfg.dir));

})
gulp.task('minify_plugin_js',function(){
    gulp.src(v1_assets.js)
        .pipe(amdOptimize("main",{
            configFile: v1_assets.require_manifest_file,
            findNestedDependencies: true,
            wrap: true,

            include: true
        }))
        // .pipe(uglifyJS())
        .pipe(concatFile('dadasay.min.js'))
        .pipe(gulp.dest('public/plugin/v1/js'));
})
