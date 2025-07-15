Tags: [[Linux]] [[Basic Commands]] 
{
	"name": "Linux Basic Commands",
	"description": "Cheatsheet for basic Linux commands",
	"author": "Chris Read",
	"email": "centurix@gmail.com",
	"repository": "http://fipo.co",
	"version": "1.0",
	"sections": {
		"File Operations": {
			"List Files": {
				"description": "List all files and directories in the current directory",
				"code": "ls"
			},
			"Change Directory": {
				"description": "Change to the specified directory",
				"code": "cd <directory>"
			},
			"Copy File": {
				"description": "Copy a file from source to destination",
				"code": "cp <source> <destination>"
			},
			"Move File": {
				"description": "Move a file from source to destination",
				"code": "mv <source> <destination>"
			},
			"Remove File": {
				"description": "Remove the specified file",
				"code": "rm <file>"
			},
			"Create Directory": {
				"description": "Create a new directory",
				"code": "mkdir <directory>"
			},
			"Remove Directory": {
				"description": "Remove an empty directory",
				"code": "rmdir <directory>"
			}
		},
		"File Viewing": {
			"View File Contents": {
				"description": "Display the contents of a file",
				"code": "cat <file>"
			},
			"View File Contents Page by Page": {
				"description": "Display the contents of a file one page at a time",
				"code": "less <file>"
			},
			"View Start of File": {
				"description": "Display the first few lines of a file",
				"code": "head <file>"
			},
			"View End of File": {
				"description": "Display the last few lines of a file",
				"code": "tail <file>"
			}
		},
		"System Information": {
			"Print Working Directory": {
				"description": "Display the current directory path",
				"code": "pwd"
			},
			"Display Disk Usage": {
				"description": "Show disk usage of files and directories",
				"code": "du"
			},
			"Display Free Disk Space": {
				"description": "Show free disk space",
				"code": "df"
			},
			"Display Process Status": {
				"description": "Display a list of currently running processes",
				"code": "ps"
			},
			"Show System Uptime": {
				"description": "Display how long the system has been running",
				"code": "uptime"
			}
		}
	}
}
