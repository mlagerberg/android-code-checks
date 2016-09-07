# android-code-checks

Various configurations for code checks for Android.

Contains modifications to the default configurations to remove silly
or senseless warnings, and to fix compatibility issues with the checker.

Uses the [Noveogroup Android Check plugin](https://github.com/noveogroup/android-check) for Gradle.

### Included code checks

* Android Lint
* Checkstyle
* Findbugs
* PMD

### Usage

1. Place the xml files of this repo into the `/config` folder in your project.
2. Add this plugin to your root, project level build.gradle: `classpath 'com.noveogroup.android:check:1.2.3'`
3. Add the following to your module level build.gradle:

		
		apply plugin: 'com.noveogroup.android.check'
		
		...
		
		android {
		
			...
			
			lintOptions {
				abortOnError false
				checkReleaseBuilds true
				lintConfig file("${project.rootDir}/config/lint.xml")
				xmlOutput file("${project.buildDir}/reports/lint/lint.xml")
				htmlOutput file("${project.buildDir}/reports/lint/lint.html")
		    }
		}

		check {
		    abortOnError false
		
		    checkstyle {
		        skip false
		        abortOnError false
		        config "${project.rootDir}/config/checkstyle.xml"
		        report new File(project.buildDir, 'reports/checkstyle')
		        reportXML new File(project.buildDir, 'reports/checkstyle/checkstyle.xml')
		        reportHTML new File(project.buildDir, 'reports/checkstyle/checkstyle.html')
		    }
		
		    pmd {
		        skip false
		        abortOnError false
		        config "${project.rootDir}/config/pmd.xml"
		        report new File(project.buildDir, 'reports/pmd')
		        reportXML new File(project.buildDir, 'reports/pmd/pmd.xml')
		        reportHTML new File(project.buildDir, 'reports/pmd/pmd.html')
		    }
		
		    findbugs {
		        // Note: set this to false when you run into this issue:
		        // https://github.com/noveogroup/android-check/issues/14
		        skip false
		        abortOnError false
		        config "${project.rootDir}/config/findbugs.xml"
		        report new File(project.buildDir, 'reports/findbugs')
		        reportXML new File(project.buildDir, 'reports/findbugs/findbugs.xml')
		        reportHTML new File(project.buildDir, 'reports/findbugs/findbugs.html')
		    }
		}
		
4. When using Jenkins, configure it to publish results using these paths:
	* **Lint**:  	`**/build/reports/lint/lint.xml`
	* **Checkstyle**: `**/build/reports/checkstyle/checkstyle.xml`
	* **Findbugs**: `**/build/reports/findbugs/findbugs.xml`
	* **PMD**: `**/build/reports/pmd/pmd.xml`
