<p>These scripts are used to build and release the content for tiddlywiki.com. They are not designed for general purpose use – they resolve problems that are specific to the task of building tiddlywiki.com: pushing to <a class="tc-tiddlylink tc-tiddlylink-missing" href="#GitHub">GitHub</a> Pages, handling the prerelease builds and bumping version numbers.</p><p>Nonetheless, you may find techniques that are useful for your own scripts.</p><h1 class="">Hosting</h1><p><a class="tc-tiddlylink-external" href="http://tiddlywiki.com" target="_blank">http://tiddlywiki.com</a> is served by <a class="tc-tiddlylink-external" href="https://pages.github.com" target="_blank">GitHub Pages</a> from the repository <a class="tc-tiddlylink-external" href="https://github.com/Jermolene/jermolene.github.io" target="_blank">https://github.com/Jermolene/jermolene.github.io</a></p><p>The scripts live in the repository <a class="tc-tiddlylink-external" href="https://github.com/Jermolene/build.jermolene.github.io" target="_blank">https://github.com/Jermolene/build.jermolene.github.io</a></p><h1 class="">Directory structure</h1><p>These scripts require the following directories to be siblings:</p><ul><li><code>build.jermolene.github.io</code> - a local copy of <a class="tc-tiddlylink-external" href="https://github.com/Jermolene/build.jermolene.github.io" target="_blank">https://github.com/Jermolene/build.jermolene.github.io</a></li><li><code>jermolene.github.io</code> - a local copy of the repo <a class="tc-tiddlylink-external" href="https://github.com/Jermolene/jermolene.github.io" target="_blank">https://github.com/Jermolene/jermolene.github.io</a></li><li><code>TiddlyWiki5</code> - a local copy of the repo <a class="tc-tiddlylink-external" href="https://github.com/Jermolene/TiddlyWiki5" target="_blank">https://github.com/Jermolene/TiddlyWiki5</a></li></ul><p>The scripts are designed to be executed with the current directory being the <code>TiddlyWiki5</code> directory.</p><h1 class="">Configuration</h1><h2 class="">package.json</h2><p>The <code>package.json</code> in the root of the <code>build.jermolene.github.io</code> repository contains a dependency declaration that specifies the latest official released version of <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a> to be used when building the release targets:</p><pre class="js hljs"><code>  <span class="hljs-string">"dependencies"</span>: {
    <span class="hljs-string">"tiddlywiki"</span>: <span class="hljs-string">"5.1.2"</span>
  }</code></pre><h2 class="">Environment variables</h2><p>Some of the scripts use the following environment variables:</p><ul><li><strong>TW5_BUILD_MAIN_EDITION</strong> - the path to the wiki folder to be used as the main edition, generating <code>index.html</code> and <code>encrypted.html</code></li><li><strong>TW5_BUILD_OUTPUT</strong> - the path to the output folder (defaults to <code>../jermolene.github.io</code>)</li><li><strong>TW5_BUILD_TIDDLYWIKI</strong> - the pathname of the <code>tiddlywiki.js</code> to be used (defaults to <code>../build.jermolene.github.io/node_modules/tiddlywiki/tiddlywiki.js</code>)</li></ul><h1 class="">Scripts</h1><h2 class=""><code>bld.sh</code></h2><p>Builds the <code>tiddlywiki.com</code> target files. By default, it uses the version of tiddlywiki specified in the <code>package.json</code> file. This can be overridden with the <strong>TW5_BUILD_TIDDLYWIKI</strong> environment variable. The following command would select the latest prerelease version of tiddlywiki from the <code>TiddlyWiki5</code> directory:</p><pre class="bash hljs"><code>    TW5_BUILD_TIDDLYWIKI=./tiddlywiki.js</code></pre><h2 class=""><code>readme-bld.sh</code></h2><p>Builds the readme files for the <code>TiddlyWiki5</code> and <code>build.jermolene.github.io</code> repos using the released version of <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a> specified in <code>package.json</code>.</p><h2 class=""><code>prerelease-bld.sh</code></h2><p>Builds the <code>tiddlywiki.com/prerelease</code> target files using the latest <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a> prerelease code and special <strong>prerelease</strong> edition for the content.</p><h2 class=""><code>github-push.sh</code></h2><p>Pushes the latest changes to the <code>jermolene.github.io</code> directory to <a class="tc-tiddlylink tc-tiddlylink-missing" href="#GitHub">GitHub</a>.</p><h2 class=""><code>dev-bld.sh</code></h2><p>Builds the <strong>dev</strong> prerelease edition.</p><h2 class=""><code>quick-bld.sh</code></h2><p>Builds the <strong>prerelease</strong> prerelease edition.</p><h2 class=""><code>tiddlyspace-upload.sh</code></h2><p>Builds the <strong>tw5tiddlyweb</strong> edition and uploads it to <a class="tc-tiddlylink tc-tiddlylink-missing" href="#TiddlySpace">TiddlySpace</a>.</p><h2 class=""><code>verbump.sh</code></h2><p>Bumps the version number of the <code>package.json</code> in the <code>TiddlyWiki5</code> repo and applies the correct version tag to the repo.</p><h2 class=""><code>npm-publish.sh</code></h2><p>Publishes the <code>TiddlyWiki5</code> repo to npm.</p><h1 class="">Procedures</h1><h2 class="">Releasing a new version of <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a></h2><ol><li>Move the latest release note from the prerelease edition into the tw5.com edition</li><li>Adjust the release date and the <strong>released</strong> field of the latest release tiddler (eg, <a class="tc-tiddlylink tc-tiddlylink-missing" href="#Release%205.1.3">Release 5.1.3</a>)</li><li>Ensure <a class="tc-tiddlylink tc-tiddlylink-missing" href="#TiddlyWiki%20Releases">TiddlyWiki Releases</a> has the new version as the default tab</li><li>Adjust the modified time of <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#HelloThere">HelloThere</a></li><li>Make sure <strong>Jermolene/<a class="tc-tiddlylink tc-tiddlylink-missing" href="#TiddlyWiki5">TiddlyWiki5</a></strong> is fully committed</li><li>Edit <code>package.json</code> to the new version number</li><li>Run <code>../build.jermolene.github.io/readme-bld.sh</code> to build the readme files</li><li>Commit the new readme files in <code>TiddlyWiki5</code> </li><li>Restore <code>package.json</code> to the previous version number</li><li>Run <code>../build.jermolene.github.io/verbump &quot;5.1.3&quot;</code> (substituting the correct version number) to update the version number, assign it a tag </li><li>Run <code>../build.jermolene.github.io/npm-publish.sh</code> to publish the release to npm</li><li>Update the <code>package.json</code> for <code>build.jermolene.github.io</code> to the new version</li><li>Verify that the new release of <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a> is available at <a class="tc-tiddlylink-external" href="https://www.npmjs.org/package/tiddlywiki" target="_blank">https://www.npmjs.org/package/tiddlywiki</a></li><li>Change current directory to the <code>build.jermolene.github.io</code> directory</li><li>Run <code>npm install</code> to install the correct version of <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a></li><li>Change current directory to the <code>TiddlyWiki5</code> directory</li><li>Run <code>../build.jermolene.github.io/bld.sh</code> to build the content files</li><li>Verify that the files in the <code>jermolene.github.io</code> directory are correct</li><li>Run <code>../build.jermolene.github.io/github-push.sh</code> to push the new files to <a class="tc-tiddlylink tc-tiddlylink-missing" href="#GitHub">GitHub</a></li><li>Run <code>../build.jermolene.github.io/tiddlyspace-upload.sh &lt;username&gt; &lt;password&gt;</code> to upload the release to <a class="tc-tiddlylink tc-tiddlylink-missing" href="#TiddlySpace">TiddlySpace</a></li><li>Tweet the release with the text &quot;<a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a> v5.x.x released to <a class="tc-tiddlylink-external" href="http://tiddlywiki.com" target="_blank">http://tiddlywiki.com</a> #newtiddlywikirelease&quot;</li><li>Preparation for the next release:<ol><li>Adjust version number in <a class="tc-tiddlylink tc-tiddlylink-shadow" href="#%24%3A%2Fconfig%2FOfficialPluginLibrary">$:/config/OfficialPluginLibrary</a></li><li>Adjust version number in <a class="tc-tiddlylink-external" href="https://github.com/Jermolene/build.jermolene.github.io" target="_blank">https://github.com/Jermolene/build.jermolene.github.io</a> in <code>prerelease-bld.sh</code>, <code>bld.sh</code> and <code>make-library-bld.sh</code></li></ol></li></ol><h2 class="">Releasing new content for <a class="tc-tiddlylink tc-tiddlylink-resolves" href="#TiddlyWiki">TiddlyWiki</a></h2><ol><li>Change current directory to the <code>TiddlyWiki5</code> directory</li><li>Run <code>../build.jermolene.github.io/bld.sh</code> to build the content files</li><li>Run <code>../build.jermolene.github.io/readme-bld.sh</code> to build the readmes</li><li>Commit the readmes to <code>TiddlyWiki5</code> and <code>build.jermolene.github.io</code> if necessary</li><li>Verify that the files in the <code>jermolene.github.io</code> directory are correct</li><li>Run <code>../build.jermolene.github.io/github-push.sh</code> to push the new files to <a class="tc-tiddlylink tc-tiddlylink-missing" href="#GitHub">GitHub</a></li></ol>