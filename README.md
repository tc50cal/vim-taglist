# vim-taglist
A Tag List plugin, which provides a source code browser for the Vim editor.

This plugin is a downstream fork of [taglist](http://www.vim.org/scripts/script.php?script_id=273) and was created by [Yegappan Lakshmanan](http://www.vim.org/account/profile.php?user_id=244)

It provides an overview of the structure of source code files and allows you 
to efficiently browse through source code files in different programming languages. 
It is the top-rated and most-downloaded plugin for the Vim editor. The taglist 
plugin groups and displays the functions, classes, structures, enumerations, macro 
definitions and other parts of a source code file in a Vim window. The taglist 
plugin will automatically highlight the current tag. You can jump to the definition 
of a tag by selecting the tag name from the taglist window. For a list of features 
supported by the taglist plugin, visit the features page.

For more information about using this plugin, after installing the 
taglist plugin, use the ":help taglist" command.

## The taglist plugin provides the following features:
  * Displays the tags (functions, classes, structures, variables, etc.) defined in a file in a vertically or horizontally split Vim window.
  * In GUI Vim, optionally displays the tags in the Tags drop-down menu and in the popup menu.
  * Automatically updates the taglist window as you switch between files/buffers. As you open new files, the tags defined in the new files are added to the existing file list and the tags defined in all the files are displayed grouped by the filename.
  * When a tag name is selected from the taglist window, positions the cursor at the definition of the tag in the source file.
  * Automatically highlights the current tag name.
  * Groups the tags by their type and displays them in a foldable tree.
  * Can display the prototype and scope of a tag.
  * Can optionally display the tag prototype instead of the tag name in the taglist window.
  * The tag list can be sorted either by name or by chronological order.
  * Supports the following language files:
  * Assembly, ASP, Awk, Beta, C, C++, C#, Cobol, Eiffel, Erlang, Fortran, HTML, Java, Javascript, Lisp, Lua, Make, Pascal, Perl, PHP, Python, Rexx, Ruby, Scheme, Shell, Slang, SML, Sql, TCL, Verilog, Vim and Yacc.
  * Can be easily extended to support new languages. Support for existing languages can be modified easily.
  * Provides functions to display the current tag name in the Vim status line or the window title bar.
  * The list of tags and files in the taglist can be saved and restored across Vim sessions.
  * Provides commands to get the name and prototype of the current tag.
  * Runs in both console/terminal and GUI versions of Vim.
  * Works with the winmanager plugin. Using the winmanager plugin, you can use Vim plugins like the file explorer, buffer explorer and the taglist plugin at the same time like an IDE.
  * Can be used in both Unix and MS-Windows systems.

## Installation

1. `apt-vim install -y https://github.com/tc50cal/vim-taglist.git`
2. Change to the $HOME/.vim/doc or $HOME/vimfiles/doc or $VIM/vimfiles/doc 
    directory, start Vim and run the ":helptags ." command to process the 
    taglist help file. Without this step, you cannot jump to the taglist help 
    topics. 
3. If the exuberant ctags utility is not present in your PATH, then set the 
    Tlist_Ctags_Cmd variable to point to the location of the exuberant ctags 
    utility (not to the directory) in the .vimrc file. 
4. If you are running a terminal/console version of Vim and the terminal 
    doesn't support changing the window width then set the 
    'Tlist_Inc_Winwidth' variable to 0 in the .vimrc file. 
5. Restart Vim. 
6. You can now use the ":TlistToggle" command to open/close the taglist 
    window. You can use the ":help taglist" command to get more information 
    about using the taglist plugin.
    
    
## Extending the taglist plugin

The taglist plugin supports all the programming languages supported by the exuberant ctags tool, which includes the following languages: Assembly, ASP, Awk, Beta, C, C++, C#, Cobol, Eiffel, Erlang, Fortran, HTML, Java, Javascript, Lisp, Lua, Make, Pascal, Perl, PHP, Python, Rexx, Ruby, Scheme, Shell, Slang, SML, Sql, TCL, Verilog, Vim and Yacc.
You can extend the taglist plugin to add support for new languages and also modify the support for the above listed languages.

You should NOT make modifications to the taglist plugin script file to add support for new languages. You will lose these changes when you upgrade to the next version of the taglist plugin. Instead you should follow the below described instructions to extend the taglist plugin.

You can extend the taglist plugin by setting variables in the .vimrc or _vimrc file. The name of these variables depends on the language name and is described below.

### Modifying support for an existing language

To modify the support for an already supported language, you have to set the tlist_xxx_settings variable in the ~/.vimrc or $HOME/_vimrc file. Replace xxx with the Vim filetype name for the language file.
To determine the filetype name used by Vim for a file, use the following command in the buffer containing the file:

    :set filetype

For example, to modify the support for the perl language files, you have to set the tlist_perl_settings variable. To modify the support for java files, you have to set the tlist_java_settings variable.

The format of the value set in the tlist_xxx_settings variable is

    <language_name>;flag1:name1;flag2:name2;flag3:name3
The different fields in the value are separated by the ';' character.
The first field 'language_name' is the name used by exuberant ctags to refer to this language file. This name can be different from the file type name used by Vim. For example, for C++, the language name used by ctags is 'c++' but the filetype name used by Vim is 'cpp'.

The remaining fields follow the format "flag:name". The sub-field 'flag' is the language specific flag used by exuberant ctags to generate the corresponding tags. For example, for the C language, to list only the functions, the 'f' flag is used. To get the list of flags supported by exuberant ctags for the various languages use the following command:

    $ ctags --list-kinds=all
The sub-field 'name' specifies the title text to use for displaying the tags of a particular type. For example, 'name' can be set to 'functions'. This field can be set to any text string name.
For example, to list only the classes and functions defined in a C++ language file, add the following line to your .vimrc file:

    let tlist_cpp_settings = 'c++;c:class;f:function'
In the above setting, 'cpp' is the Vim filetype name and 'c++' is the name used by the exuberant ctags tool. 'c' and 'f' are the flags passed to exuberant ctags to list C++ classes and functions and 'class' is the title used for the class tags and 'function' is the title used for the function tags in the taglist window.
For example, to display only functions defined in a C file and to use "My Functions" as the title for the function tags, use

    let tlist_c_settings = 'c;f:My Functions'
When you set the tlist_xxx_settings variable, you will override the default setting used by the taglist plugin for the 'xxx' language. You cannot add to the default options used by the taglist plugin for a particular file type. To add to the options used by the taglist plugin for a language, copy the option values to your .vimrc file.
Adding support for a new language

If you want to add support for a new language to the taglist plugin, you need to first extend the exuberant ctags tool. For more information about extending exuberant ctags, visit the extending exuberant ctags page.
To add support for a new language, set the tlist_xxx_settings variable appropriately as described above. Replace 'xxx' in the variable name with the Vim filetype name for the new language.

For example, to extend the taglist plugin to support the latex language, you can use the following line (assuming, you have already extended exuberant ctags to support the latex language):

    let tlist_tex_settings='latex;b:bibitem;c:command;l:label'
With the above line, when you edit files of filetype "tex" in Vim, the taglist plugin will invoke the exuberant ctags tool passing the "latex" filetype and the flags b, c and l to generate the tags. The text heading 'bibitem', 'command' and 'label' will be used in the taglist window for the tags which are generated for the flags b, c and l respectively.
Language specific extensions

The extensions to exuberant ctags and the taglist plugin to support additional programming languages are listed below. These extensions are contributed by users of the taglist plugin.

### ActionScript 
Add the following lines to the $HOME/.ctags or $HOME/ctags.conf file:
```
    --langdef=actionscript
    --langmap=actionscript:.as
    --regex-actionscript=/^[ \t]*[(private| public|static) ( \t)]*function[ \t]+([A-Za-z0-9_]+)[ \t]*\(/\1/f, function, functions/
    --regex-actionscript=/^[ \t]*[(public) ( \t)]*function[ \t]+(set|get) [ \t]+([A-Za-z0-9_]+)[ \t]*\(/\1 \2/p,property, properties/
    --regex-actionscript=/^[ \t]*[(private| public|static) ( \t)]*var[ \t]+([A-Za-z0-9_]+)[ \t]*/\1/v,variable, variables/
    --regex-actionscript=/.*\.prototype \.([A-Za-z0-9 ]+)=([ \t]?)function( [ \t]?)*\(/\1/ f,function, functions/
    --regex-actionscript=/^[ \t]*class[ \t]+([A-Za-z0-9_]+)[ \t]*/\1/c,class, classes/
```
Add the following lines to the ~/.vimrc or $HOME\_vimrc file:
" actionscript language
let tlist_actionscript_settings = 'actionscript;c:class;f:method;p:property;v:variable'
### Latex 
Add the following lines to the $HOME/.ctags or $HOME/ctags.conf file:
```
    --langdef=latex
    --langmap=latex:.tex
    --regex-latex=/^\\part[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/PART \2/s,part/
    --regex-latex=/^\\part[[:space:]]*\*[[:space:]]*\{([^}]+)\}/PART \1/s,part/
    --regex-latex=/^\\chapter[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/CHAP \2/s,chapter/
    --regex-latex=/^\\chapter[[:space:]]*\*[[:space:]]*\{([^}]+)\}/CHAP \1/s,chapter/
    --regex-latex=/^\\section[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/\. \2/s,section/
    --regex-latex=/^\\section[[:space:]]*\*[[:space:]]*\{([^}]+)\}/\. \1/s,section/
    --regex-latex=/^\\subsection[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/\.\. \2/s,subsection/
    --regex-latex=/^\\subsection[[:space:]]*\*[[:space:]]*\{([^}]+)\}/\.\. \1/s,subsection/
    --regex-latex=/^\\subsubsection[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/\.\.\. \2/s,subsubsection/
    --regex-latex=/^\\subsubsection[[:space:]]*\*[[:space:]]*\{([^}]+)\}/\.\.\. \1/s,subsubsection/
    --regex-latex=/^\\includegraphics[[:space:]]*(\[[^]]*\])?[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/\3/g,graphic+listing/
    --regex-latex=/^\\lstinputlisting[[:space:]]*(\[[^]]*\])?[[:space:]]*(\[[^]]*\])?[[:space:]]*\{([^}]+)\}/\3/g,graphic+listing/
    --regex-latex=/\\label[[:space:]]*\{([^}]+)\}/\1/l,label/
    --regex-latex=/\\ref[[:space:]]*\{([^}]+)\}/\1/r,ref/
    --regex-latex=/\\pageref[[:space:]]*\{([^}]+)\}/\1/p,pageref/
    --regex-make=/^([^:# \t]+)[ \t]*[:]{1,2}/\1/t,targets/
```
Add the following lines to the ~/.vimrc or $HOME\_vimrc file:
let tlist_tex_settings   = 'latex;s:sections;g:graphics;l:labels'
let tlist_make_settings  = 'make;m:makros;t:targets'

## Taglist plugin todo list
  * Group tags according to the scope and display them. For example, group all the tags belonging to a C++/Java class
  * When opening a new Vim tab, automatically open the taglist window.
  * Support for displaying tags in a modified (not-yet-saved) file.
  * Automatically open the taglist window only for selected filetypes. For other filetypes, close the taglist window.
  * When using the shell from the MKS toolkit, the taglist plugin doesn't work.
  * The taglist plugin doesn't work with files edited remotely using the netrw plugin. The exuberant ctags utility cannot process files over scp/rcp/ftp, etc.
